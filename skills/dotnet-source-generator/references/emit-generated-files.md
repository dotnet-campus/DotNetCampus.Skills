---
name: emit-generated-files
description: 如何让编译器将源生成器输出写入磁盘文件，以便 AI 或开发者直接阅读和验证生成结果
metadata:
  type: reference
---

# 将源生成器输出保存到磁盘

## 为什么需要这么做

源生成器的输出默认只存在于编译过程的内存中。将其保存到磁盘后，AI 就能直接阅读生成的代码，验证源生成器的行为是否正确。

## 推荐方式：命令行参数

直接在编译时传递属性，无需修改任何源代码：

```bash
dotnet build /p:EmitCompilerGeneratedFiles=true
```

生成的文件默认输出到中间输出目录：

```
obj/Debug/net8.0/generated/{程序集名}/{源生成器类型全名}/{生成的文件名}
```

例如：`obj/Debug/net8.0/generated/MyApp.Generators/MyApp.Generators.MyGenerator/UserService.g.cs`

这是 AI 开发源生成器时的首选方式——不修改项目文件，只是临时查看生成结果。

## 备选方式：项目文件配置

如果项目希望始终输出生成的文件（例如纳入源代码管理），可以在 `.csproj` 中添加：

```xml
<PropertyGroup>
    <EmitCompilerGeneratedFiles>true</EmitCompilerGeneratedFiles>
</PropertyGroup>
```

## 延伸阅读

如果以上信息不足以解决你遇到的问题（例如需要自定义输出路径、处理多目标框架、或将生成文件纳入源代码管理），请阅读：

https://andrewlock.net/creating-a-source-generator-part-6-saving-source-generator-output-in-source-control/
