# ExcelUnlock - Excel密码破解工具

ExcelUnlock 是一个功能强大的命令行工具，用于破解受密码保护的 Excel 文件。它支持多种破解模式，包括单密码验证、字典攻击、暴力破解和掩码模式。

> **免责声明：** 本项目仅供代码学习和研究使用，禁止用于非法用途。使用本工具造成的任何后果由使用者自行承担。

> **姊妹项目：** 需要处理 PDF 密码或限制？请看 [PDFUnlock](https://github.com/houyongsheng/PDFUnlock) —— 同系列的 PDF 密码破解 / 去限制工具。

## 功能特点

- 支持多种破解模式
- 详细的进度显示
- 自动保存解密后的文件
- 支持断点续传
- 多线程并行处理
- 内存使用优化

## 系统要求

- .NET 8.0 或更高版本
- 支持的操作系统：Windows, macOS, Linux

## 安装方法

1. 克隆仓库：
```bash
git clone https://github.com/houyongsheng/ExcelUnlock.git
```

2. 进入项目目录：
```bash
cd ExcelUnlock-master
```

3. 编译项目：
```bash
dotnet build
```

## 使用方法

### 1. 单密码模式
用于验证单个密码：
```bash
dotnet run -- -f "Excel文件路径.xlsx" -m SinglePassword -p "要尝试的密码"
```

示例：
```bash
dotnet run -- -f "test.xlsx" -m SinglePassword -p "1234"
```

### 2. 字典攻击模式
使用密码字典文件进行破解：
```bash
dotnet run -- -f "Excel文件路径.xlsx" -m Dictionary -d "密码字典文件.txt"
```

示例：
```bash
dotnet run -- -f "test.xlsx" -m Dictionary -d "passwords.txt"
```

### 3. 暴力破解模式
尝试所有可能的密码组合：
```bash
dotnet run -- -f "Excel文件路径.xlsx" -m BruteForce --min 4 --max 6 --charset "0123456789"
```

参数说明：
- --min：最小密码长度
- --max：最大密码长度
- --charset：使用的字符集

### 4. 掩码模式
使用特定模式破解密码：
```bash
dotnet run -- -f "Excel文件路径.xlsx" -m Mask --mask "?d?d?d?d"
```

掩码规则：
- ?d = 数字 (0-9)
- ?l = 小写字母 (a-z)
- ?u = 大写字母 (A-Z)
- ?s = 特殊字符

### 通用选项

- --resume：从上次中断处继续（true/false）
- --save-state：保存破解状态（true/false）

## 注意事项

1. 文件格式支持
   - 目前仅支持 .xlsx 格式的 Excel 文件
   - 文件必须是使用标准加密方式加密

2. 性能考虑
   - 暴力破解模式可能需要较长时间
   - 建议先尝试单密码模式或字典攻击模式
   - 可以使用 --save-state 选项保存进度

3. 安全提示
   - 仅用于合法用途
   - 请确保您有权限访问要破解的文件

## 错误处理

程序会显示详细的错误信息，包括：
- 文件格式检查
- 加密类型识别
- 密码验证结果
- 文件访问错误

## 开发说明

### 依赖包
- NPOI (2.6.2)
- BouncyCastle.Cryptography (2.2.1)
- DocumentFormat.OpenXml (3.0.0)

### 主要类和方法
- Program.cs：主程序入口
- TryPassword：密码验证核心方法
- SaveUnencrypted：解密文件保存方法

## 许可证

本项目采用 MIT 许可证。查看 [LICENSE](LICENSE) 文件了解更多信息。

## 贡献指南

1. Fork 项目
2. 创建特性分支
3. 提交更改
4. 推送到分支
5. 创建 Pull Request

## 常见问题

Q: 为什么显示"文件未加密"？
A: 文件可能未设置密码保护或使用了不支持的加密方式。

Q: 程序运行很慢怎么办？
A: 建议先使用字典模式，如果没有结果再使用暴力破解模式。可以通过设置较小的密码长度范围来提高效率。

Q: 是否支持 .xls 格式？
A: 目前仅支持 .xlsx 格式，后续版本可能会添加对其他格式的支持。
