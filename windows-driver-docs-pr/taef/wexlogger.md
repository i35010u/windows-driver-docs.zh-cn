---
title: WexLogger
description: WexLogger
ms.assetid: D9F4AD08-19EA-4a6c-AD25-886FBEA334B8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4270d21d5b4ca1313e50d54c97a355cd3b9c179f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546821"
---
# <a name="wexlogger"></a>WexLogger


WexLogger 为日志记录的跨越本机代码，托管的代码和脚本提供一致的 API。 它还可从一直到长期持续压力测试的命令提示中运行单元测试。

## <a name="logging-through-the-verify-framework"></a>通过日志记录验证框架


应通过执行测试用例中的大多数日志记录[验证](verify.md)框架。 这将确保测试以更清晰、 更连续且用户可读的方式创作。 但是，在某些情况下，测试作者将发现他们需要围绕写入日志的内容更精细的控制： 因此 WexLogger API 的需要。

## <a name="logging-within-taef"></a>TAEF 中的日志记录


对于 TAEF 内运行的测试用例，没有任何记录器初始化需要由测试的作者。 您可以立即开始使用 Log API 公开的语言，创作中的测试。

在本机 c + + 代码中，它将如下所示：

```cpp
using namespace WEX::Logging;
using namespace WEX::Common;
Log::Comment(L"Rendering to the BufferView");
Log::Comment(L"Render succeeded");

Log::Comment(String().Format(L"Look, a number! %d", aNumber));

#define LOG_OUTPUT(fmt, ...) Log::Comment(String().Format(fmt, __VA_ARGS__))
LOG_OUTPUT(L"Look, a number! %d", aNumber);
```

在托管代码中，它将如下所示：

```cpp
Log.Comment("Rendering to the BufferView");
Log.Comment("Render succeeded");
```

在 JScript 中，它将如下所示：

```cpp
var log = new ActiveXObject("WEX.Logger.Log");
log.Comment("Rendering to the BufferView");
log.Comment("Render succeeded");
```

## <a name="logging-outside-taef"></a>日志记录外部 TAEF


大多数情况下，初始化和完成日志记录将执行 TAEF，因此 WexLogger 将可供使用的测试用例持续时间内，如上所述，并将正确完成。 但是，如果客户端想要使用外部 TAEF WexLogger，它们将负责手动调用**LogController::InitializeLogging()** 并**LogController::FinalizeLogging()**。 对于本机和托管代码; 仅存在这一要求脚本不具有此附加要求。 LogController api，请参阅详细信息如下静态 LogController 方法表。

请参阅[生成 WTT 日志](#generating-wtt-logs)部分，了解如何生成外部 TAEF WTT 日志的信息。

## <a name="wexlogger-api"></a>WexLogger API


**下面是可用的本机 c + + 日志方法列表。**

有相应的版本可供托管的代码和脚本。

| 本机 c + + 日志方法                                                                                                              | 功能                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Assert(const wchar\_t\* pszAssert)                                                                                                  | 记录测试断言。                                                                                                                                                                           |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszContext)                                                                     | 与上下文记录测试 assert。                                                                                                                                                             |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)                                | 日志测试断言与文件、 函数和行信息。                                                                                                                                  |
| Assert(const wchar\_t\* pszAssert, const wchar\_t\* pszContext, const wchar\_t\* pszFile, const wchar\_t\* pszFunction, int line)   | 记录测试 assert 的上下文中，以及文件中，函数和行信息。                                                                                                               |
| Bug(const wchar\_t\* pszBugDatabase, int bugId)                                                                                     | 记录已知的 bug 数。                                                                                                                                                                      |
| Bug(const wchar\_t\* pszBugDatabase, int bugId, const wchar\_t\* pszContext)                                                        | 与上下文记录已知的错误号。                                                                                                                                                        |
| Comment(const wchar\_t\* pszComment)                                                                                                | 记录测试注释。                                                                                                                                                                          |
| Comment(const wchar\_t\* pszComment, const wchar\_t\* pszContext)                                                                   | 日志测试注释，与上下文                                                                                                                                                             |
| EndGroup(const wchar\_t\* pszGroupName)                                                                                             | 登录组或特定测试的测试，结尾。                                                                                                                                      |
| EndGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext)                                                                | 与上下文日志组的测试，或特定测试的结尾。                                                                                                                        |
| Error(const wchar\_t\* pszError)                                                                                                    | 记录测试错误。                                                                                                                                                                            |
| Error(const wchar\_t\* pszError, const wchar\_t\* pszContext)                                                                       | 记录测试错误，与上下文。                                                                                                                                                              |
| 错误 (const wchar\_t\* pszError，const wchar\_t\* pszFile，const wchar\_t\* pszFunction，int 行)                                  | 记录测试错误与文件、 函数和行信息。                                                                                                                                   |
| 错误 (const wchar\_t\* pszError，const wchar\_t\* pszContext，const wchar\_t\* pszFile，const wchar\_t\* pszFunction，int 行)     | 记录测试错误，使用上下文，以及文件中，函数和行信息。                                                                                                                |
| File(const wchar\_t\* pszFileName)                                                                                                  | 日志要保存的测试文件。 文件保存到&lt;WTTRunWorkingDir&gt;\\WexLogFileOutput （如果设置 WTTRunWorkingDir），或&lt;CurrentDirectory\\&gt;WexLogFileOutput。               |
| File(const wchar\_t\* pszFileName, const wchar\_t\* pszContext)                                                                     | 记录要与上下文一起保存的测试文件。 文件保存到&lt;WTTRunWorkingDir&gt;\\WexLogFileOutput （如果设置 WTTRunWorkingDir），或&lt;CurrentDirectory\\&gt;WexLogFileOutput。 |
| Property(const wchar\_t\* pszName, const wchar\_t\* pszValue)                                                                       | 名称/值属性对用户身份登录。 值可以是 xml 格式。                                                                                                                              |
| Property(const wchar\_t\* pszName, const wchar\_t\* pszValue, const wchar\_t\* pszContext)                                          | 记录与上下文的名称/值属性对。 值可以是 xml 格式。                                                                                                                |
| Result(TestResults::Result testResult)                                                                                              | 记录测试结果。                                                                                                                                                                           |
| Result(TestResults::Result testResult, const wchar\_t\* pszComment)                                                                 | 带有关联的注释记录测试结果。                                                                                                                                                |
| Result(TestResults::Result testResult, const wchar\_t\* pszComment, const wchar\_t\* pszContext)                                    | 带有关联的注释，与上下文记录测试结果。                                                                                                                                  |
| StartGroup(const wchar\_t\* pszGroupName)                                                                                           | 登录组或特定测试的测试，开始。                                                                                                                                    |
| StartGroup(const wchar\_t\* pszGroupName, TestResults::Result defaultTestResult)                                                    | 登录组或特定的测试; 的测试开始此外会设置默认测试结果。                                                                                                 |
| StartGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext)                                                              | 登录组或特定测试的测试，开始与上下文。                                                                                                                      |
| StartGroup(const wchar\_t\* pszGroupName, const wchar\_t\* pszContext, TestResults::Result defaultTestResult)                       | 登录组或特定的测试; 的测试开始此外会设置默认测试结果。                                                                                                 |
| Warning(const wchar\_t\* pszWarning)                                                                                                | 记录测试警告。                                                                                                                                                                          |
| Warning(const wchar\_t\* pszWarning, const wchar\_t\* pszContext)                                                                   | 与上下文记录测试警告。                                                                                                                                                            |
| 警告 (const wchar\_t\* pszWarning，const wchar\_t\* pszFile，const wchar\_t\* pszFunction，int 行)                              | 使用文件、 函数和行信息记录测试警告。                                                                                                                                 |
| 警告 (const wchar\_t\* pszWarning，const wchar\_t\* pszContext，const wchar\_t\* pszFile，const wchar\_t\* pszFunction，int 行) | 记录测试警告，使用上下文，以及文件中，函数和行信息。                                                                                                              |
| Xml(const wchar\_t\* pszXml)                                                                                                        | 日志的 xml 数据。 不会进行检查以验证它格式正确。                                                                                                                             |
| Xml(const wchar\_t\* pszXml, const wchar\_t\* pszContext)                                                                           | Xml 数据，记录与上下文。 不会进行检查以验证它格式正确。                                                                                                               |
| MiniDump()                                                                                                                          | 记录当前进程小型转储。                                                                                                                                                           |



**注意：**"上下文"是一个额外的字符串，你可以选择提供与**WexLogger** API 调用，以提供更多上下文或详细信息。 例如，你可以选择始终传入"ImageComparator"作为您的上下文时产生任何**WexLogger** ImageComparator 类方法的 API 调用。

下面是本机 c + + 的可能有效值**TestResults::Result**枚举。 有相应的版本可供托管的代码和脚本。

| 本机 c + + TestResults::Result 枚举 | 功能        |
|--------------------------------------------|----------------------|
| 传递                                     | 测试已通过      |
| NotRun                                     | 不运行测试 |
| 已跳过                                    | 已跳过测试 |
| 已阻止                                    | 测试已被阻止 |
| Failed                                     | 测试失败      |



**下面是可用的本机 c + + LogContoller 方法列表：**

| 本机 c + + LogController 方法                                                                       | 功能                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态 HRESULT InitializeLogging()                                                                     | 初始化日志记录功能。                                                                                                                                                                                                                                                                               |
| 静态 HRESULT InitializeLogging(WexLoggerErrorCallback pfnErrorCallback)                              | 初始化日志记录功能，并指定你想要使用的内部记录器错误通知的 WexLoggerErrorCallback 函数。                                                                                                                                                               |
| static HRESULT InitializeLogging(const wchar\_t\* pszLogName)                                          | 初始化日志记录功能，并指定你想要使用的日志文件的名称。 **注意：** 日志名称仅考虑到，如果[启用 WttLogging](#generating-wtt-logs)。                                                                                                             |
| 静态 HRESULT InitializeLogging(const wchar\_t\* pszLogName, WexLoggerErrorCallback pfnErrorCallback) | 初始化日志记录功能中，指定你想要使用，并指定你想要使用的内部记录器错误通知的 WexLoggerErrorCallback 函数的日志文件的名称。 **注意：** 日志名称仅考虑到，如果[启用 WttLogging](#generating-wtt-logs)。 |
| static bool IsInitialized()                                                                            | LogController 已初始化，此过程返回。                                                                                                                                                                                                                                 |
| 静态 const unsigned short\* GetLogName()                                                             | 返回指定了在 InitializeLogging 调用中的日志 （如果有） 的名称。                                                                                                                                                                                                                         |
| 静态 HRESULT FinalizeLogging()                                                                       | 完成日志记录功能。                                                                                                                                                                                                                                                                                   |



**注意：** 请参阅 c + + 错误处理部分下面的详细信息**WexLoggerErrorCallback**机制以及如何使用外部 TAEF 框架。

**注意：** 它只是用来使用时调用 InitializeLogging/FinalizeLogging **WexLogger**之外 TAEF 框架作为 TAEF 已处理了处理日志记录初始化/完成。

**注意：** 不需要初始化/完成日志记录功能时使用**WexLogger**从脚本。

**下面是可用的本机 c + + RemoteLogContoller 方法列表：**

| 本机 c + + RemoteLogController 方法                                                                             | 功能                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态 HRESULT GenerateConnectionData(WEX::Common::NoThrowString& connectionData)                                  | 生成必须父和子进程中使用，以允许子进程，以便返回到父进程的连接数据。                                                          |
| 静态 HRESULT GenerateConnectionData(const wchar\_t\* pszMachineName, WEX::Common::NoThrowString& connectionData) | 启动远程计算机上的子进程时使用。 生成必须父和子进程中使用，以允许子进程，以便返回到父进程的连接数据。 |
| 静态 HRESULT InitializeLogging(WEX::Common::NoThrowString connectionData)                                        | 初始化日志记录中的父进程的功能，因此子进程可以返回到该记录。                                                                                                         |



**注意：** 请参阅[远程日志记录从子进程](#remote-logging-from-child-processes)部分获取远程日志记录的详细信息。

下面是可用的托管日志方法列表。

| 托管的日志方法                                                             | 功能                                                                                                                                                                |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 断言 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)         | 使用特定于区域性的格式设置信息提供程序、 一个格式字符串，并包含零个或多个要格式化的对象的对象数组的一个测试断言的日志。               |
| 断言 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)         | 使用特定于区域性的格式设置信息提供程序、 一个格式字符串，并包含零个或多个要格式化的对象的对象数组的一个测试断言的日志。               |
| 断言 （字符串消息）                                                          | 记录测试断言。                                                                                                                                                           |
| 断言 （字符串格式、 对象 arg0）                                              | 日志测试断言使用的格式字符串和对象设置格式。                                                                                                             |
| 断言 (字符串格式、 params 对象\[\] args)                                   | 使用一个格式字符串，测试断言的日志，并且包含零个或多个要格式化的对象的对象数组。                                                                   |
| 断言 （字符串消息、 字符串上下文中）                                          | 与上下文记录测试 assert。                                                                                                                                             |
| Assert （字符串消息、 字符串文件、 字符串函数、 int 行）                  | 记录测试断言，以及文件中，函数和行信息。                                                                                                             |
| Assert （字符串消息、 字符串上下文中，字符串文件、 字符串函数、 int 行）  | 记录测试 assert 的上下文中，以及文件中，函数和行信息。                                                                                               |
| Bug （字符串 bugDatabase，int bugId）                                              | 记录已知的 bug 数。                                                                                                                                                      |
| Bug （字符串 bugDatabase，int bugId，字符串上下文中）                              | 与上下文记录已知的错误号。                                                                                                                                        |
| 注释 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)        | 记录测试注释使用的区域性特定格式设置信息提供程序、 一个格式字符串和一个对象数组，包含零个或多个要格式化的对象。              |
| 注释 （字符串消息）                                                         | 测试注释日志                                                                                                                                                           |
| 注释 （字符串格式、 对象 arg0）                                             | 记录测试注释使用的格式字符串和对象设置格式。                                                                                                            |
| 注释 (字符串格式、 params 对象\[\] args)                                  | 记录测试注释使用的格式字符串和一个对象数组，包含零个或多个要格式化的对象。                                                                   |
| 注释 （字符串消息、 字符串上下文中）                                         | 日志测试注释，与上下文                                                                                                                                             |
| EndGroup(string groupName)                                                      | 登录组或特定测试的测试，结尾。                                                                                                                      |
| EndGroup(string groupName, string context)                                      | 与上下文日志组的测试，或特定测试的结尾。                                                                                                        |
| 错误 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)          | 记录测试错误使用特定于区域性的格式设置信息提供程序、 一个格式字符串和一个对象数组，包含零个或多个要格式化的对象。                |
| 错误 （字符串消息）                                                           | 记录测试错误。                                                                                                                                                            |
| 错误 （字符串格式，对象 arg0）                                               | 记录测试错误使用格式字符串和对象设置格式。                                                                                                              |
| 错误 （字符串消息，字符串上下文中）                                           | 记录测试错误，与上下文。                                                                                                                                              |
| 错误 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)          | 记录测试错误使用格式字符串和一个对象数组，包含零个或多个要格式化的对象。                                                                     |
| 错误 （字符串消息、 字符串文件、 字符串函数，int 行）                   | 记录测试错误与文件、 函数和行信息。                                                                                                                   |
| 错误 （字符串消息、 字符串上下文中，字符串文件、 字符串函数，int 行）   | 记录测试错误，使用上下文，以及文件中，函数和行信息。                                                                                                |
| 文件 (字符串 fileName)                                                           | 日志要保存的测试文件。 文件将保存到任一 WTTRunWorkingDir\\WexLogFileOutput （如果设置 WTTRunWorkingDir） 或 CurrentDirectory\\WexLogFileOutput。               |
| 文件 （字符串文件名、 字符串上下文中）                                           | 记录要与上下文一起保存的测试文件。 文件将保存到任一 WTTRunWorkingDir\\WexLogFileOutput （如果设置 WTTRunWorkingDir） 或 CurrentDirectory\\WexLogFileOutput。 |
| MiniDump()                                                                      | 记录当前进程小型转储。                                                                                                                                           |
| 属性 （字符串名称，字符串值）                                             | 名称/值属性对用户身份登录。 值可以是 xml 格式。                                                                                                              |
| 属性 （字符串名称，字符串值，字符串上下文中）                             | 记录与上下文的名称/值属性对。 值可以是 xml 格式。                                                                                                |
| 结果 (TestResult testResult)                                                   | 记录测试结果。                                                                                                                                                           |
| 结果 （TestResult testResult，字符串注释）                                   | 带有关联的注释记录测试结果。                                                                                                                                |
| 结果 （TestResult testResult、 字符串注释、 字符串上下文中）                   | 带有关联的注释，与上下文记录测试结果。                                                                                                                  |
| StartGroup(string groupName)                                                    | 登录组或特定测试的测试，开始。                                                                                                                    |
| StartGroup(string groupName, string context)                                    | 登录组或特定测试的测试，开始与上下文。                                                                                                      |
| 警告 (IFormatProvider 提供程序，字符串格式，params 对象\[\] args)        | 记录测试警告使用特定于区域性的格式设置信息提供程序、 一个格式字符串和一个对象数组，包含零个或多个要格式化的对象。              |
| 警告 （字符串消息）                                                         | 记录测试警告。                                                                                                                                                          |
| 警告 （字符串格式、 对象 arg0）                                             | 记录测试警告使用格式字符串和对象设置格式。                                                                                                            |
| 警告 (字符串格式、 params 对象\[\] args)                                  | 记录测试警告使用格式字符串和一个对象数组，包含零个或多个要格式化的对象。                                                                   |
| 警告 （字符串消息、 字符串上下文中）                                         | 与上下文记录测试警告。                                                                                                                                            |
| 警告 （字符串消息，字符串文件、 字符串函数，int 行）                 | 使用文件、 函数和行信息记录测试警告。                                                                                                                 |
| 警告 （字符串消息，字符串上下文中，字符串文件、 字符串函数，int 行） | 记录测试警告，使用上下文，以及文件中，函数和行信息。                                                                                              |
| Xml (字符串 xmlData)                                                             | 日志的 xml 数据。 不会进行检查以验证它格式正确。                                                                                                             |
| Xml （字符串 xmlData，字符串上下文中）                                             | Xml 数据，记录与上下文。 不会进行检查以验证它格式正确。                                                                                               |



**下面是可用的托管 LogContoller 方法列表：**

| 托管的 LogController 方法                 | 功能                                                                                                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static void InitializeLogging()               | 初始化日志记录功能。                                                                                                                                                                   |
| 静态 void InitializeLogging (字符串 logName) | 初始化日志记录功能，并指定你想要使用的日志文件的名称。 **注意：** 日志名称仅考虑到，如果[启用 WttLogging](#generating-wtt-logs)。 |
| static bool IsInitialized()                   | LogController 已初始化，此过程返回。                                                                                                                     |
| 静态字符串 GetLogName()                    | 返回指定了在 InitializeLogging 调用中的日志 （如果有） 的名称。                                                                                                             |
| 静态 void FinalizeLogging()                 | 完成日志记录功能。                                                                                                                                                                       |



**注意：** 有关如何处理错误和异常使用的托管的层时，请参阅托管代码错误和异常下面的部分的详细信息**WexLogger** TAEF framework 外部。

**注意：** 它只是用来使用时调用 InitializeLogging/FinalizeLogging **WexLogger**之外 TAEF 框架作为 TAEF 已处理了处理日志记录初始化/完成。

**注意：** 不需要初始化/完成日志记录功能时使用**WexLogger**从脚本。

**下面是可用的托管 RemoteLogContoller 方法列表：**

| 托管的 RemoteLogController 方法                      | 功能                                                                                                                                                                                                |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态字符串 GenerateConnectionData()                   | 生成必须父和子进程中使用，以允许子进程，以便返回到父进程的连接数据。                                                          |
| 静态字符串 GenerateConnectionData(string machineName) | 启动远程计算机上的子进程时使用。 生成必须父和子进程中使用，以允许子进程，以便返回到父进程的连接数据。 |
| 静态 void InitializeLogging (字符串 connectionData)     | 初始化日志记录中的父进程的功能，因此子进程可以返回到该记录。                                                                                                         |



**注意：** 请参阅[远程日志记录从子进程](#remote-logging-from-child-processes)部分获取远程日志记录的详细信息。

## <a name="remote-logging-from-child-processes"></a>从子进程的远程日志记录


WexLogger 提供的功能的一个或更多的子进程来记录回单个父进程，导致生成单个日志文件中的合并的测试结果。

父进程的同一台计算机或远程另一台计算机上可以运行的子进程。 为远程计算机日志记录正常工作，负责 WexLogger 客户端，若要在远程计算机上添加 TCP 防火墙例外的所有子进程。 但是，如果在父级所在的同一计算机上运行的子进程，不则需要防火墙进行任何修改。

以下步骤所需设置远程日志记录的每个连接：

**父进程**

1.  调用**RemoteLogController::GenerateConnectionData()** 生成这两个进程必须用于启动日志记录连接的连接数据。

    **注意：** 请务必检查此调用的返回值。

    ```cpp
        NoThrowString connectionData;
        Throw::IfFailed(RemoteLogController::GenerateConnectionData(connectionData));

    ```

2.  通过将其设置在其环境块中，或将其作为自变量在命令提示符下传递通信与子进程的连接数据。 例如：

    **将作为 WexLogger 能够理解的命令提示符处的命名参数传递：**  
    /wexlogger\_connectiondata=*\[connection data\]*

    **注意：** 如果使用此选项，然后步骤 1**子进程**以下部分**不是**必要。

    **将作为 WexLogger 能够理解的名称的环境变量传递：**  
    \[YourAppName\_cmd\]=/wexlogger\_connectiondata=*\[connection data\]*

    **注意：** 如果使用此选项，然后步骤 1**子进程**以下部分**不是**必要。

    **将传递到进程中以任意格式 （某些其他命令参数、 环境变量等。）**  
    **注意：** 如果使用此选项，然后步骤 1**子进程**以下部分**是**必要。

    **注意：** 为方便起见，值"/ wexlogger\_connectiondata ="定义为在本机和托管 RemoteLogControllers 常量：

    -   **WEX::Logging::c\_szWexLoggerRemoteConnectionData**，LogController.h 中

    -   **RemoteLogController.WexLoggerRemoteConnectionData**，Wex.Logger.Interop.dll 中

3.  启动子进程使用的连接数据
4.  调用**RemoteLogController::InitalizeLogging (*\[在步骤 1 中创建的连接数据\]*)**。 必须进行此调用，启动子进程，因为它将超时，如果子不会调用后**LogController::InitializeLogging()** 及时。

    **注意：** 请务必检查此调用的返回值。

    ```cpp
    // ...launch child process with connection data...
    Throw::IfFailed(RemoteLogController::InitializeLogging(connectionData));
    ```

5.  等待子进程，等等。

**子进程**

1.  如果已连接数据**不**传递到子进程为命名参数在命令提示符下该 WexLogger 能够识别 （请参阅上述步骤 2），则必须设置这种情况下的环境变量：

    \[YourAppName\_cmd\]=/wexlogger\_connectiondata=*\[connection data\]*

    **例如：**

    ```cpp
    // App name is mytestapp.exe
    ::SetEnvironmentVariable(L"mytestapp_cmd", String(c_szWexLoggerRemoteConnectionData).Append(connectionData));
    ```

2.  调用**LogController::InitializeLogging()** 初始化该进程的日志记录。 在内部，这将利用上述第 1 步中设置的环境变量 (或中的步骤 2**父进程**部分) 启动返回到父进程的日志记录连接。
3.  日志，等等;所有跟踪将都发回给父进程。
4.  调用**LogController::FinalizeLogging()** 来完成此过程的日志记录。

## <a name="determining-test-outcome"></a>确定测试结果


尽管没有提供显式声明的测试用例预期的结果的方法 (**日志:: Result()**)，没有任何**需要**测试用例以在大多数情况下使用此方法。

例如，如果测试用例不显式调用**日志:: Result()**，并**却不**记录错误 (通过**日志:: Error()**)，默认情况下它被视为传递测试用例; 如果它**does**日志错误，这是一个失败测试案例。

但是，如果测试用例**does**显式调用**Log::Result(TestResults::TestPassed)**，但还**does**记录错误中测试用例、 测试仍将进行计数为失败由于测试中出错。

内部 TAEF 框架中，可以通过标记包含不同的默认测试结果的测试写此行为。 可以在"创作 TAEF Tests"文档中找到对此的详细信息。

此外可以通过显式调用重写此行为**日志:: StartGroup()** 为你自己测试组/测试用例，默认值测试所选的结果。

## <a name="generating-wtt-logs"></a>生成 WTT 日志


存在三种方法来生成通过 WTT 日志**WexLogger**。 所有这些要求**WttLog.dll**是存在于运行目录，或在你的路径。

-   如果运行的在实验室中，使用 wtt 客户端安装，则会自动为您生成 wtt 日志。 这是由于 WexLogger 看起来应仅存在于实验室环境中的两个环境变量存在：WttTaskGuid 和 WTTRunWorkingDir。 如果这两项存在，会自动启用 wtt 日志记录。
-   如果实验室环境外部运行 TAEF 内，请将在命令提示符下 /enablewttlogging 传递给测试用例。 示例：

    ``` syntax
    te my.test.dll /enablewttlogging
    ```

-   如果您正在使用 WexLogger framework 外部的 TAEF，并且你未在实验室环境中运行，必须设置 **&lt;YOUR\_进程\_名称&gt;\_CMD**环境变量包含此选项在调用之前**LogController::InitializeLogging()**。 示例：
    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

-   如果你想要附加到现有的 wtt 日志文件，而不是覆盖它，还指定除了 /enablewttlogging /appendwttlogging 选项。

    ``` syntax
    te my.test.dll /enablewttlogging /appendwttlogging
    ```

    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging /appendwttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging /appendwttlogging");
    LogController.InitializeLogging();
    ```

还有可能完全覆盖或追加到默认 WttLogger 设备字符串通过指定下列命令选项之一：

/ WttDeviceString:&lt;新设备字符串&gt;   
完全重写时初始化 WttLogger 使用 WexLogger WttDeviceString。

/ WttDeviceStringSuffix:&lt;要追加到设备字符串值&gt;   
为默认值时初始化 WttLogger 使用 WexLogger WttDeviceString 追加指定的值。 如果已忽略 / WttDeviceString 同时指定。

下表列出了 WexLogger 测试结果如何映射到 WttLogger 结果：

| WexLogger | WttLogger                      |
|-----------|--------------------------------|
| 传递    | WTT\_TESTCASE\_RESULT\_PASS    |
| NotRun    | WTT\_TESTCASE\_RESULT\_BLOCKED |
| 已跳过   | WTT\_测试用例\_结果\_已跳过 |
| 已阻止   | WTT\_TESTCASE\_RESULT\_BLOCKED |
| Failed    | WTT\_TESTCASE\_RESULT\_FAIL    |



## <a name="logger-dependencies"></a>记录器的依赖项


本机 c + + 记录器 (**Wex.Logger.dll**) 依赖于**Wex.Common.dll**并**Wex.Communication.dll**。

托管的记录器 (**Wex.Logger.Interop.dll**) 依赖于**Wex.Logger.dll**， **Wex.Common.dll**和**Wex.Communication.dll**.

此外， **WttLog.dll** Wtt 日志记录已启用时是必需的。

## <a name="additional-error-data"></a>其他错误数据


事件中记录一个错误，可以启用 WexLogger 以包含一个或多个与错误本身除了以下各项：

-   MiniDump
-   ScreenCapture
-   StackTrace

``` syntax
te my.test.dll /minidumponerror
```

``` syntax
te my.test.dll /screencaptureonerror /stacktraceonerror
```

通过一个或多个已启用这些选项，您将收到额外输出每次调用日志:: Error()。

注意：如果您正在使用 WexLogger TAEF 框架之外，则必须设置 **&lt;YOUR\_进程\_名称&gt;\_CMD**环境变量来包含这些选项然后再调用**LogController::InitializeLogging()**。 示例：

```cpp
Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

```cpp
Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

## <a name="c-error-handling"></a>C + + 错误处理


若要屏蔽的不必检查每个日志 API 调用的返回值的测试用例作者，WexLogger 报告意外的错误状态通过使用可选的回调机制;**WexLoggerErrorCallback**函数。 后的 initializaiton **WexLogger** (通过**LogController::InitializeLogging()**)，客户端可以选择指定**WexLoggerErrorCallback**时调用函数在出现意外的错误条件**WexLogger**。 **WexLoggerErrorCallback**函数必须使用以下签名：

```cpp
void __stdcall MyLoggerErrorCallback(const unsigned short* pszMessage, HRESULT hr);
```

WexLoggerErrorCallback 函数的一个常见用途是写出到控制台的错误消息 （如果你的测试工具是一个控制台应用程序）。 例如，TAEF framework 是的客户端**WexLogger**，并实现**WexLoggerErrorCallback**其中在 WexLogger 错误发生时，红色文本写入到控制台。

## <a name="net-40-compatibility"></a>.NET 4.0 兼容性


Wex.Logger.Interop 编译为 NetFx 2/3/3.5 二进制文件，以便它可以加载到 NetFx 2/3/3.5 和 4 的 NetFx 进程。 这允许 TAEF 运行上面的 NetFx 2 的所有托管程序集。 如果使用 Wex.Logger 外部 TAEF，则需要将添加[配置文件](https://msdn.microsoft.com/library/ms229689.aspx)exe 配置 NetFx 4 运行时将加载到它的 NetFx 2/3/3.5 二进制文件是过程。 配置文件应包含以下信息：

```cpp
<configuration> 
    <startup useLegacyV2RuntimeActivationPolicy="true">
        <supportedRuntime version="v4.0"/>
    </startup>
</configuration>
```

## <a name="managed-code-error-and-exception-handling"></a>托管的代码错误和异常处理


若要屏蔽的每个检查返回值的负担从测试用例作者**日志**API 调用 WexLogger 托管的层会报告意外的错误状态通过使用**LoggerController.WexLoggerError**事件。 您可能会订阅此事件在任何时候通过实现您自己**WexLoggerErrorEventHandler**并使用以下熟悉语法用于C#事件订阅：

```cpp
LogController.WexLoggerError += new WexLoggerEventHandler(My_WexLoggerErrorHandler);
```

下面是示例的事件处理程序可能如下所示：

```cpp
static void LogController_WexLoggerError(object sender, WexLoggerErrorEventArgs e)
{
    ConsoleColor originalColor = Console.ForegroundColor;
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("LogController_WexLoggerError: " + e.Message);
    Console.ForegroundColor = originalColor;
}
```

此外， **LogController::InitializeLogging()** 并**LogController::FinalizeLogging()** 方法本身发生故障时引发 WexLoggerException。 这提供了该错误的详细的信息，并且还可以中止测试运行开始之前。 测试用例作者将永远不需要担心如何捕获这些异常-应 WexLogger initializaiton/完成期间仅应处理。









