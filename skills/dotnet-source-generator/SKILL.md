---
name: dotnet-source-generator
description: 帮助 AI 理解和开发 .NET/C# 源生成器（Source Generator）项目。当用户的项目包含源生成器，或用户正在开发、调试、修改源生成器时使用此技能。涵盖源生成器的开发、调试、验证生成输出等关键环节。即使用户没有明确提到"源生成器"，只要项目中存在 ISourceGenerator 或 IIncrementalGenerator 的实现，也应使用此技能。
---

# .NET 源生成器（Source Generator）开发技能

## 源生成器是什么

源生成器是 .NET 编译器平台（Roslyn）的一项功能，允许在编译期间分析用户代码并生成额外的 C# 源文件参与编译。源生成器以 NuGet 包或项目引用的方式集成到目标项目中。

## AI 面对源生成器的核心挑战

源生成器的输出默认只存在于编译过程的内存中，不会写入磁盘文件。这意味着 AI 无法直接看到源生成器的实际输出结果，也无法在修改源生成器后验证生成结果是否正确。

解决方法：通过 `EmitCompilerGeneratedFiles` 属性，可以让编译器将源生成器输出写入磁盘，从而让 AI 能够阅读和验证生成的代码。具体配置方法参阅 [references/emit-generated-files.md](references/emit-generated-files.md)。

## 工作流程：开发或修改源生成器时

1. 编译项目并启用输出：`dotnet build /p:EmitCompilerGeneratedFiles=true`
2. 阅读输出目录中的生成文件，验证生成结果是否符合预期
3. 如果需要修改源生成器逻辑，修改后重新编译，再次检查输出

## 专业知识参考

以下参考文档提供各个方面的详细信息，按需阅读：

| 文档 | 内容 |
|------|------|
| [references/emit-generated-files.md](references/emit-generated-files.md) | 将源生成器输出保存到磁盘的配置方法 |
| [references/skill-writing-principles.md](references/skill-writing-principles.md) | 为本技能添加新文档时应遵循的撰写原则 |
