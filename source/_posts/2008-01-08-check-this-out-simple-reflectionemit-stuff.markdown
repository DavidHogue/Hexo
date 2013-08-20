---
author: David Hogue
comments: false
date: 2008-01-08 08:00:05+00:00
layout: post
slug: check-this-out-simple-reflectionemit-stuff
title: Check This Out (Simple Reflection.Emit Stuff)
wordpress_id: 252
categories:
- Software Development
tags:
- old-blog
- reflection
---

public class HelloModifier
    {
        public static Target CreateTarget()
        {
            AssemblyName assemblyName = new AssemblyName("MyDynamic");
            TypeBuilder typeBuilder = AppDomain.CurrentDomain.
                DefineDynamicAssembly(assemblyName,
                    AssemblyBuilderAccess.Run).
                DefineDynamicModule(assemblyName.Name).
                DefineType("TargetOverride", TypeAttributes.Class,
                    typeof(Target));
            MethodBuilder hello = typeBuilder.DefineMethod("Hello",
                MethodAttributes.Public | MethodAttributes.HideBySig |
                MethodAttributes.NewSlot | MethodAttributes.Virtual,
                CallingConventions.Standard, typeof (string), 
                Type.EmptyTypes);
            ILGenerator il = hello.GetILGenerator();
            il.Emit(OpCodes.Ldstr, "Hello, World!");
            il.Emit(OpCodes.Ret);
            typeBuilder.DefineMethodOverride(hello, 
                typeof(Target).GetMethod("Hello"));
            return (Target)Activator.CreateInstance(
                typeBuilder.CreateType());
        }
    }
    
    public class Target
    {
        public virtual string Hello()
        {
            return "sorry";
        }
    }
    
    [TestFixture]
    public class NeatTests
    {
        [Test]
        public void SayHello()
        {
            Target target = HelloModifier.CreateTarget();
            Assert.AreEqual("Hello, World!", target.Hello());
        }
    }



OK, so it's not that revolutionary, but I've never had to dig into the Reflection.Emit namespaces before.  I tried once before, but never got that far.  It does seem hard to find good, useful documentation and examples on it.

This isn't really all that useful here, but I could come up with some imaginative uses for it if it was more dynamic.

Oh, and with [DynamicProxy](http://www.castleproject.org/dynamicproxy/index.html) HelloModifier looks like this:

    
    public class HelloModifier
    {
        private static readonly ProxyGenerator _generator = 
            new ProxyGenerator();
    
        public static Target CreateTarget()
        {
            return (Target)_generator.CreateClassProxy(
                typeof(Target), new HelloInterceptor());
        }
    
        private class HelloInterceptor : IInterceptor
        {
            public void Intercept(IInvocation invocation)
            {
                if (invocation.Method.Name == "Hello")
                    invocation.ReturnValue = "Hello, World!";
            }
        }
    }
