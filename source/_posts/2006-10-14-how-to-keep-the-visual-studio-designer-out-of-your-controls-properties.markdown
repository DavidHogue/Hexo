---
author: David Hogue
comments: false
date: 2006-10-14 21:06:12+00:00
layout: post
slug: how-to-keep-the-visual-studio-designer-out-of-your-controls-properties
title: How to Keep the Visual Studio Designer Out of Your Control's Properties
wordpress_id: 168
categories:
- Software Development
tags:
- old-blog
---

Do you create custom controls for Windows Forms projects?  Do you add properties to those controls?  If so, you'll probably want to apply a few attributes to those properties: Browsable and DesignerSerializationVisibility.  Else, the designer will put brain dead default values in them.

So, here's my control:


    
    Public Class MyControl
        Inherits UserControl
    
        Private m_aBoolean As Boolean = True
    
        Public Property ABoolean() As Boolean
            Get
                Return m_aBoolean
            End Get
            Set(ByVal value As Boolean)
                m_aBoolean = value
            End Set
        End Property
    
        private m_aCustomObject As MyCustomObject = New MyCustomObject()
    
        Public Property ACustomObject() As MyCustomObject
            Get
                Return m_aCustomObject 
            End Get
            Set(ByVal value As MyCustomObject)
                m_aCustomObject = value
            End Set
        End Property
        
    End Class



Then, the designer creates this:

    
    Me.MyControl1.Anchor = System.Windows.Forms.AnchorStyles.Top
    Me.MyControl1.Location = New System.Drawing.Point(10, 10)
    Me.MyControl1.Size = New System.Drawing.Size(200, 200)
    Me.MyControl1.Name = "MyControl1"
    Me.MyControl1.TabIndex = 1
    Me.MyControl1.ABoolean = True
    Me.MyControl1.ACustomObject = CType(resources.GetObject("MyControl1.ACustomObject "), The.Whole.NameSpace.MyCustomObject)



The boolean is mostly harmless, but annoying because it just set the default value.  Not too useful.

Far worse is the custom object.  The designer actually took my custom object and binary serialized it and stuffed it in the MyControl.resx file as base64 encoded text.  If I change any fields in my custom object (rename, add, remove) the compile will fail with something like:

`error 2	Invalid Resx file. Could not load type The.Whole.NameSpace.MyCustomObject, TestProject, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null which is used in the .RESX file.  Ensure that the necessary references have been added to your project. Line 136, position 5.	C:codeTestProjectSomeControl.resx	136	5	TestProject`

The updated code that doesn't allow the designer to muck up the properties:


    
    Imports System.ComponentModel
    
    Public Class MyControl
        Inherits UserControl
    
        Private m_aBoolean As Boolean = True
    
        <Browsable(False)> _
        <DesignerSerializationVisibility(DesignerSerializationVisibility.Content)> _
        Public Property ABoolean() As Boolean
            Get
                Return m_aBoolean
            End Get
            Set(ByVal value As Boolean)
                m_aBoolean = value
            End Set
        End Property
    
        private m_aCustomObject As MyCustomObject = New MyCustomObject()
    
        <Browsable(False)> _
        <DesignerSerializationVisibility(DesignerSerializationVisibility.Content)> _
        Public Property ACustomObject() As MyCustomObject
            Get
                Return m_aCustomObject 
            End Get
            Set(ByVal value As MyCustomObject)
                m_aCustomObject = value
            End Set
        End Property
        
    End Class



The <Browsable> attribute simply stops it from showing up in the properties window.  The <DesignerSerializationVisibility> attribute stops the designer from writing code for the property.

You will want to remove the lines from the .Designer and .Resx file that look like:


    
    <data mimetype="application/x-microsoft.net.object.binary.base64" name="SubClassEditControl.Item">
        <value>
            AAEAAAD/////AQAAAAAAAAAEAQAAABxTeXN0ZW0uQ29sbGVjdGlvbnMuQXJyYXlMaXN0AwAAAAZfaXRl
            bXMFX3NpemUIX3ZlcnNpb24FAAAICAkCAAAAAAAAAAAAAAAQAgAAAAAAAAAL
    </value>
      </data>



Another option, for the boolean anyway, is to specify the default value.  That way the designer will only set it if it is changed from the property window.


    
    <DefaultValue(True)> _
    Public Property ABoolean() As Boolean
        Get
            Return m_aBoolean
        End Get
        Set(ByVal value As Boolean)
            m_aBoolean = value
        End Set
    End Property
