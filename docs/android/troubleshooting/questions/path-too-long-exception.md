---
title: "How do I resolve a PathTooLongException error?"
description: "This article explains how to resolve a PathTooLongException that may occur while building an app."
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 60EE1C8D-BE44-4612-B3B5-70316D71B1EA
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/20/2018
---
 
# How do I resolve a PathTooLongException error?

## Cause

Generated path names in a Xamarin.Android project can be quite long.
For example, a path like the following could be generated during a
build:

**C:\\Some\\Directory\\Solution\\Project\\obj\\Debug\\__library_projects__\\Xamarin.Forms.Platform.Android\\library_project_imports\\assets**

On Windows (where the maximum length for a path is
[260 characters](https://msdn.microsoft.com/library/windows/desktop/aa365247.aspx)),
a **PathTooLongException** could be produced while building the
project if a generated path exceeds the maximum length. 

## Fix

Beginning with Xamarin.Android 8.0, the `UseShortFileNames` MSBuild
property can be set to circumvent this error. When this property is set
to `True` (the default is `False`), the build process uses shorter path
names to reduce the likelihood of producing a **PathTooLongException**.
For example, when `UseShortFileNames` is set to `True`, the above path
is shortened to path that is similar to the following:

**C:\\Some\\Directory\\Solution\\Project\\obj\\Debug\\lp\\1\\jl\\assets**

To set this property, add the following MSBuild property to the
project **.csproj** file:

```xml
<PropertyGroup>
    <UseShortFileNames>True</UseShortFileNames>
</PropertyGroup>
```

For more information about setting build properties, see
[Build Process](~/android/deploy-test/building-apps/build-process.md).
