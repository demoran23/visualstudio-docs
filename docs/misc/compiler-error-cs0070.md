---
title: "Compiler Error CS0070 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0070"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0070"
ms.assetid: bb0de7c6-c734-4a8f-ab62-0a50eac2a91f
caps.latest.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Compiler Error CS0070
The event 'event' can only appear on the left hand side of += or -= (except when used from within the type 'type')  
  
 Outside of the class it is defined in, an [event](/dotnet/csharp/language-reference/keywords/event) can only add or subtract references. For more information, see [Events](/dotnet/csharp/programming-guide/events/index).  
  
 The following sample generates CS0070:  
  
```  
// CS0070.cs  
using System;  
public delegate void EventHandler();  
  
public class A  
{  
   public event EventHandler Click;  
  
   public static void OnClick()  
   {  
      EventHandler eh;  
      A a = new A();  
      eh = a.Click;  
   }  
  
   public static void Main()  
   {  
   }  
}  
  
public class B  
{  
   public int Foo ()  
   {  
      EventHandler eh = new EventHandler(A.OnClick);  
      A a = new A();  
      eh = a.Click;   // CS0070  
      // try the following line instead  
      // a.Click += eh;  
      return 1;  
   }  
}  
```