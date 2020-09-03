---
title: WexLogger
description: WexLogger
ms.assetid: D9F4AD08-19EA-4a6c-AD25-886FBEA334B8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13697f4b74205b754df6716bfeb47ffa40d2c417
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402698"
---
# <a name="wexlogger"></a>WexLogger


WexLogger 提供一致的 API，用于记录跨越本机代码、托管代码和脚本的情况。 它还可从命令提示符下运行的单元测试一直到长到长距离的压力测试。

## <a name="logging-through-the-verify-framework"></a>通过验证框架进行日志记录


测试用例中的大多数日志记录应通过 [验证](verify.md) 框架执行。 这将确保以更清晰、更有序和可读取的方式编写测试。 但是，在某些情况下，测试作者会发现他们需要更精细地控制写入日志的内容：因此需要 WexLogger API。

## <a name="logging-within-taef"></a>TAEF 中的日志记录


对于在 TAEF 中运行的测试用例，测试作者不需要进行记录器初始化。 你可以立即开始使用日志 API，该 API 公开给你要在其中创作测试的语言。

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

## <a name="logging-outside-taef"></a>在 TAEF 外部登录


大多数情况下，日志记录初始化和完成将由 TAEF 执行，因此，WexLogger 将随时可用于测试用例的持续时间，如前文所述，并将正确完成。 但是，如果客户端想要在 TAEF 外部使用 WexLogger，则他们将负责手动调用 **LogController：： InitializeLogging ( # B1 ** 和 **LogController：： FinalizeLogging ( # B3 **。 此要求仅适用于本机和托管代码;脚本没有此附加要求。 有关 LogController API 的详细信息，请参阅下面的静态 LogController 方法表。

有关如何在 TAEF 之外生成 WTT 日志的信息，请参阅 [生成 WTT 日志](#generating-wtt-logs) 部分。

## <a name="wexlogger-api"></a>WexLogger API


**下面是可用的本机 c + + 日志方法的列表。**

托管代码和脚本可使用等效版本。

| 本机 c + + 日志方法                                                                                                              | 功能                                                                                                                                                                                |
|-------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Assert (const wchar \_ t \* pszAssert)                                                                                                   | 记录测试断言。                                                                                                                                                                           |
| Assert (const wchar \_ t \* pszAssert，const wchar \_ t \* pszContext)                                                                      | 使用上下文记录测试断言。                                                                                                                                                             |
| Assert (const wchar \_ t \* pszAssert，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)                                 | 使用文件、函数和行信息记录测试断言。                                                                                                                                  |
| Assert (const wchar \_ t \* pszAssert，const wchar \_ t \* pszContext，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)    | 使用上下文和文件、函数和行信息记录测试断言。                                                                                                               |
| Bug (const wchar \_ t \* pszBugDatabase，int bugId)                                                                                      | 记录已知的 bug 号。                                                                                                                                                                      |
| Bug (const wchar \_ t \* pszBugDatabase，int bugId，const wchar \_ t \* pszContext)                                                         | 使用上下文记录已知的 bug 号。                                                                                                                                                        |
| Comment (const wchar \_ t \* pszComment)                                                                                                 | 记录测试备注。                                                                                                                                                                          |
| Comment (const wchar \_ t \* pszComment，const wchar \_ t \* pszContext)                                                                    | 使用上下文记录测试注释                                                                                                                                                             |
| EndGroup (const wchar \_ t \* pszGroupName)                                                                                              | 记录一组测试或特定测试的结束。                                                                                                                                      |
| EndGroup (const wchar \_ t \* pszGroupName，const wchar \_ t \* pszContext)                                                                 | 使用上下文记录一组测试或特定测试的结束。                                                                                                                        |
| 错误 (const wchar \_ t \* pszError)                                                                                                     | 记录测试错误。                                                                                                                                                                            |
| 错误 (const wchar \_ t \* pszError，const wchar \_ t \* pszContext)                                                                        | 使用上下文记录测试错误。                                                                                                                                                              |
| 错误 (const wchar \_ t \* pszError，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)                                   | 记录包含文件、函数和行信息的测试错误。                                                                                                                                   |
| 错误 (const wchar \_ t \* pszError，const wchar \_ t \* pszContext，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)      | 记录测试错误和上下文，以及文件、函数和行信息。                                                                                                                |
| 文件 (const wchar \_ t \* pszFileName)                                                                                                   | 记录要保存的测试文件。 &lt; &gt; \\ 如果 WTTRunWorkingDir 设置) 或 &lt; CurrentDirectory \\ &gt; WexLogFileOutput，则文件将保存到 WTTRunWorkingDir WexLogFileOutput (。               |
| File (const wchar \_ t \* pszFileName，const wchar \_ t \* pszContext)                                                                      | 使用上下文记录要保存的测试文件。 &lt; &gt; \\ 如果 WTTRunWorkingDir 设置) 或 &lt; CurrentDirectory \\ &gt; WexLogFileOutput，则文件将保存到 WTTRunWorkingDir WexLogFileOutput (。 |
| Property (const wchar \_ t \* pszName，const wchar \_ t \* pszValue)                                                                        | 记录名称/值属性对。 该值可以是 xml 格式。                                                                                                                              |
| Property (const wchar \_ t \* pszName，const wchar \_ t \* pszValue，const wchar \_ t \* pszContext)                                           | 使用上下文记录名称/值属性对。 该值可以是 xml 格式。                                                                                                                |
| Result (TestResults：： Result testResult)                                                                                               | 记录测试结果。                                                                                                                                                                           |
| Result (TestResults：： Result testResult，const wchar \_ t \* pszComment)                                                                  | 使用关联的注释记录测试结果。                                                                                                                                                |
| Result (TestResults：： Result testResult，const wchar \_ t \* pszComment，const wchar \_ t \* pszContext)                                     | 使用上下文的关联注释记录测试结果。                                                                                                                                  |
| StartGroup (const wchar \_ t \* pszGroupName)                                                                                            | 记录一组测试或特定测试的启动。                                                                                                                                    |
| StartGroup (const wchar \_ t \* PszGroupName，TestResults：： Result defaultTestResult)                                                     | 记录一组测试或特定测试的开始;还设置默认测试结果。                                                                                                 |
| StartGroup (const wchar \_ t \* pszGroupName，const wchar \_ t \* pszContext)                                                               | 使用上下文记录一组测试或特定测试的启动。                                                                                                                      |
| StartGroup (const wchar \_ t \* pszGroupName，const wchar \_ t \* pszContext，TestResults：： Result defaultTestResult)                        | 记录一组测试或特定测试的开始;还设置默认测试结果。                                                                                                 |
| 警告 (const wchar \_ t \* pszWarning)                                                                                                 | 记录测试警告。                                                                                                                                                                          |
| 警告 (const wchar \_ t \* pszWarning，const wchar \_ t \* pszContext)                                                                    | 使用上下文记录测试警告。                                                                                                                                                            |
| 警告 (const wchar \_ t \* pszWarning，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)                               | 使用文件、函数和行信息记录测试警告。                                                                                                                                 |
| 警告 (const wchar \_ t \* pszWarning，const wchar \_ t \* pszContext，const wchar \_ t \* pszFile，const wchar \_ t \* pszFunction，int line)  | 记录测试警告和上下文，还记录文件、函数和行信息。                                                                                                              |
| Xml (const wchar \_ t \* pszXml)                                                                                                         | 记录 xml 数据。 不进行检查以验证它是否格式正确。                                                                                                                             |
| Xml (const wchar \_ t \* pszXml，const wchar \_ t \* pszContext)                                                                            | 记录 xml 数据和上下文。 不进行检查以验证它是否格式正确。                                                                                                               |
| 小型转储 ( # A1                                                                                                                          | 记录当前进程的小型转储。                                                                                                                                                           |



**注意：** "上下文" 是一种额外的字符串，你可以选择通过 **WexLogger** API 调用提供此字符串，以提供更多上下文或详细信息。 例如，在从 ImageComparator 类方法进行任何 **WexLogger** API 调用时，可以选择始终将 "ImageComparator" 作为上下文传入。

以下为本机 c + + **TestResults：： Result** 枚举的有效值。 托管代码和脚本可使用等效版本。

| Native c + + TestResults：： Result 枚举 | 功能        |
|--------------------------------------------|----------------------|
| Passed                                     | 已通过测试      |
| NotRun                                     | 测试未运行 |
| 已跳过                                    | 已跳过测试 |
| 已阻止                                    | 已阻止测试 |
| 失败                                     | 测试失败      |



**下面是可用的本机 c + + LogController 方法列表：**

| 本机 c + + LogController 方法                                                                       | 功能                                                                                                                                                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态 HRESULT InitializeLogging ( # A1                                                                     | 初始化日志记录功能。                                                                                                                                                                                                                                                                               |
| 静态 HRESULT InitializeLogging (WexLoggerErrorCallback pfnErrorCallback)                               | 初始化日志记录功能，并指定想要用于接收内部记录器错误通知的 WexLoggerErrorCallback 函数。                                                                                                                                                               |
| 静态 HRESULT InitializeLogging (const wchar \_ t \* pszLogName)                                           | 初始化日志记录功能，并指定要使用的日志文件的名称。 **注意：** 仅当 [启用了 WttLogging 时](#generating-wtt-logs)才考虑日志名称。                                                                                                             |
| static HRESULT InitializeLogging (const wchar \_ t \* PszLogName，WexLoggerErrorCallback pfnErrorCallback)  | 初始化日志记录功能，指定你想要使用的日志文件的名称，并指定你想要用于接收内部记录器错误通知的 WexLoggerErrorCallback 函数。 **注意：** 仅当 [启用了 WttLogging 时](#generating-wtt-logs)才考虑日志名称。 |
| static bool IsInitialized ( # A1                                                                            | 返回是否已为此进程初始化 LogController。                                                                                                                                                                                                                                 |
| static const 无符号 short \* GetLogName ( # A1                                                             | 如果任何) ，则返回为 InitializeLogging (调用中的日志指定的名称。                                                                                                                                                                                                                         |
| 静态 HRESULT FinalizeLogging ( # A1                                                                       | 完成日志记录功能。                                                                                                                                                                                                                                                                                   |



**注意：** 有关 **WexLoggerErrorCallback** 机制的详细信息以及如何在 TAEF 框架之外使用该机制，请参阅下面的 c + + 错误处理部分。

**注意：** 只有在 TAEF framework 外使用 **WexLogger** 时，才需要调用 InitializeLogging/FinalizeLogging，因为 TAEF 已经处理了日志记录初始化/完成。

**注意：** 使用脚本中的 **WexLogger** 时，不需要初始化/完成日志记录功能。

**下面是可用的本机 c + + RemoteLogContoller 方法列表：**

| 本机 c + + RemoteLogController 方法                                                                             | 功能                                                                                                                                                                                                |
|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态 HRESULT GenerateConnectionData (WEX：： Common：： NoThrowString& connectionData)                                   | 生成必须在父进程和子进程内使用的连接数据，以允许子进程重新登录到父进程。                                                          |
| 静态 HRESULT GenerateConnectionData (const wchar \_ t \* PSZMACHINENAME，WEX：： Common：： NoThrowString& connectionData)  | 在远程计算机上启动子进程时使用。 生成必须在父进程和子进程内使用的连接数据，以允许子进程重新登录到父进程。 |
| 静态 HRESULT InitializeLogging (WEX：： Common：： NoThrowString connectionData)                                         | 初始化父进程中的日志记录功能，以便子进程可以重新登录。                                                                                                         |



**注意：** 有关远程日志记录的详细信息，请参阅下面的 [从子进程远程日志记录](#remote-logging-from-child-processes) 部分。

下面是可用的托管日志方法列表。

| 托管日志方法                                                             | 功能                                                                                                                                                                |
|---------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 断言 (IFormatProvider 提供程序、字符串格式、参数对象 \[ \] 参数)          | 使用特定于区域性的格式设置信息提供程序、格式字符串和包含要设置格式的零个或多个对象的对象数组记录测试断言。               |
| 断言 (IFormatProvider 提供程序、字符串格式、参数对象 \[ \] 参数)          | 使用特定于区域性的格式设置信息提供程序、格式字符串和包含要设置格式的零个或多个对象的对象数组记录测试断言。               |
| 断言 (字符串消息)                                                           | 记录测试断言。                                                                                                                                                           |
| 断言 (字符串格式，对象 arg0)                                               | 使用格式字符串和要设置格式的对象记录测试断言。                                                                                                             |
| 断言 (字符串格式，参数对象 \[ \] 参数)                                    | 使用格式字符串记录测试断言，并使用包含零个或多个要设置格式的对象的对象数组。                                                                   |
| 断言 (字符串消息，字符串上下文)                                           | 使用上下文记录测试断言。                                                                                                                                             |
| 断言 (字符串消息、字符串文件、字符串函数、int 行)                   | 记录测试断言，还记录文件、函数和行信息。                                                                                                             |
| 断言 (字符串消息、字符串上下文、字符串文件、字符串函数、int 行)   | 使用上下文和文件、函数和行信息记录测试断言。                                                                                               |
| Bug (字符串 bugDatabase，int bugId)                                               | 记录已知的 bug 号。                                                                                                                                                      |
| Bug (字符串 bugDatabase，int bugId，string context)                               | 使用上下文记录已知的 bug 号。                                                                                                                                        |
| 注释 (IFormatProvider 提供程序，字符串格式，参数对象 \[ \] 参数)         | 使用特定于区域性的格式设置信息提供程序、格式字符串和包含要设置格式的零个或多个对象的对象数组记录测试注释。              |
| 注释 (字符串消息)                                                          | 记录测试注释                                                                                                                                                           |
| 注释 (字符串格式，对象 arg0)                                              | 使用格式字符串和要设置格式的对象记录测试注释。                                                                                                            |
| 注释 (字符串格式，参数对象 \[ \] 参数)                                   | 使用格式字符串和包含零个或多个要设置格式的对象的对象数组记录测试注释。                                                                   |
| 注释 (字符串消息，字符串上下文)                                          | 使用上下文记录测试注释                                                                                                                                             |
| EndGroup (字符串的名)                                                       | 记录一组测试或特定测试的结束。                                                                                                                      |
| EndGroup (字符串名、string 上下文)                                       | 使用上下文记录一组测试或特定测试的结束。                                                                                                        |
| 错误 (IFormatProvider 提供程序，字符串格式，参数对象 \[ \] 参数)           | 使用特定于区域性的格式设置信息提供程序、格式字符串和包含要设置格式的零个或多个对象的对象数组记录测试错误。                |
| 错误 (字符串消息)                                                            | 记录测试错误。                                                                                                                                                            |
| 错误 (字符串格式，对象 arg0)                                                | 使用格式字符串和要设置格式的对象记录测试错误。                                                                                                              |
| 错误 (字符串消息，字符串上下文)                                            | 使用上下文记录测试错误。                                                                                                                                              |
| 错误 (IFormatProvider 提供程序，字符串格式，参数对象 \[ \] 参数)           | 使用格式字符串和包含零个或多个要设置格式的对象的对象数组记录测试错误。                                                                     |
| 错误 (字符串消息、字符串文件、字符串函数、int 行)                    | 记录包含文件、函数和行信息的测试错误。                                                                                                                   |
| 错误 (字符串消息、字符串上下文、字符串文件、字符串函数、int 行)    | 记录测试错误和上下文，以及文件、函数和行信息。                                                                                                |
| 文件 (字符串文件名)                                                            | 记录要保存的测试文件。 \\如果 WTTRunWorkingDir 设置) 或 CurrentDirectory WexLogFileOutput，则文件将保存到 WTTRunWorkingDir WexLogFileOutput (\\ 。               |
| 文件 (字符串文件名，字符串上下文)                                            | 使用上下文记录要保存的测试文件。 \\如果 WTTRunWorkingDir 设置) 或 CurrentDirectory WexLogFileOutput，则文件将保存到 WTTRunWorkingDir WexLogFileOutput (\\ 。 |
| 小型转储 ( # A1                                                                      | 记录当前进程的小型转储。                                                                                                                                           |
| 属性 (字符串名称，字符串值)                                              | 记录名称/值属性对。 该值可以是 xml 格式。                                                                                                              |
| 属性 (字符串名称、字符串值、字符串上下文)                              | 使用上下文记录名称/值属性对。 该值可以是 xml 格式。                                                                                                |
| Result (TestResult testResult)                                                    | 记录测试结果。                                                                                                                                                           |
| Result (TestResult testResult，string comment)                                    | 使用关联的注释记录测试结果。                                                                                                                                |
| Result (TestResult testResult，string comment，string context)                    | 使用上下文的关联注释记录测试结果。                                                                                                                  |
| StartGroup (字符串的名)                                                     | 记录一组测试或特定测试的启动。                                                                                                                    |
| StartGroup (字符串名、string 上下文)                                     | 使用上下文记录一组测试或特定测试的启动。                                                                                                      |
| 警告 (IFormatProvider 提供程序，字符串格式，参数对象 \[ \] 参数)         | 使用特定于区域性的格式设置信息提供程序、格式字符串和包含要设置格式的零个或多个对象的对象数组记录测试警告。              |
| 警告 (字符串消息)                                                          | 记录测试警告。                                                                                                                                                          |
| 警告 (字符串格式，对象 arg0)                                              | 使用格式字符串和要设置格式的对象记录测试警告。                                                                                                            |
| 警告 (字符串格式，参数对象 \[ \] 参数)                                   | 使用格式字符串和包含零个或多个要设置格式的对象的对象数组记录测试警告。                                                                   |
| 警告 (字符串消息，字符串上下文)                                          | 使用上下文记录测试警告。                                                                                                                                            |
| 警告 (字符串消息、字符串文件、字符串函数、int 行)                  | 使用文件、函数和行信息记录测试警告。                                                                                                                 |
| 警告 (字符串消息、字符串上下文、字符串文件、字符串函数、int 行)  | 记录测试警告和上下文，还记录文件、函数和行信息。                                                                                              |
| Xml (字符串 xmlData)                                                              | 记录 xml 数据。 不进行检查以验证它是否格式正确。                                                                                                             |
| Xml (字符串 xmlData，字符串上下文)                                              | 记录 xml 数据和上下文。 不进行检查以验证它是否格式正确。                                                                                               |



**下面是可用的托管 LogContoller 方法列表：**

| 托管 LogController 方法                 | 功能                                                                                                                                                                                       |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| static void InitializeLogging ( # A1               | 初始化日志记录功能。                                                                                                                                                                   |
| static void InitializeLogging (String logName)  | 初始化日志记录功能，并指定要使用的日志文件的名称。 **注意：** 仅当 [启用了 WttLogging 时](#generating-wtt-logs)才考虑日志名称。 |
| static bool IsInitialized ( # A1                   | 返回是否已为此进程初始化 LogController。                                                                                                                     |
| 静态字符串 GetLogName ( # A1                    | 如果任何) ，则返回为 InitializeLogging (调用中的日志指定的名称。                                                                                                             |
| static void FinalizeLogging ( # A1                 | 完成日志记录功能。                                                                                                                                                                       |



**注意：** 请参阅下面的托管代码错误和异常部分，详细了解如何在 TAEF 框架外使用 **WexLogger** 的托管层时处理错误和异常。

**注意：** 只有在 TAEF framework 外使用 **WexLogger** 时，才需要调用 InitializeLogging/FinalizeLogging，因为 TAEF 已经处理了日志记录初始化/完成。

**注意：** 使用脚本中的 **WexLogger** 时，不需要初始化/完成日志记录功能。

**下面是可用的托管 RemoteLogContoller 方法列表：**

| 托管 RemoteLogController 方法                      | 功能                                                                                                                                                                                                |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 静态字符串 GenerateConnectionData ( # A1                   | 生成必须在父进程和子进程内使用的连接数据，以允许子进程重新登录到父进程。                                                          |
| 静态字符串 GenerateConnectionData (字符串 machineName)  | 在远程计算机上启动子进程时使用。 生成必须在父进程和子进程内使用的连接数据，以允许子进程重新登录到父进程。 |
| static void InitializeLogging (String connectionData)      | 初始化父进程中的日志记录功能，以便子进程可以重新登录。                                                                                                         |



**注意：** 有关远程日志记录的详细信息，请参阅下面的 [从子进程远程日志记录](#remote-logging-from-child-processes) 部分。

## <a name="remote-logging-from-child-processes"></a>子进程的远程日志记录


WexLogger 提供一个或多个子进程登录到单个父进程的功能，导致在单个日志文件中生成合并的测试结果。

子进程可以在父进程所在的同一台计算机上运行，也可以在其他计算机上以远程方式运行。 要使远程计算机日志记录正常工作，WexLogger 客户端需要为远程计算机上的所有子进程添加 TCP 防火墙排除项。 但是，如果子进程在与父进程相同的计算机上运行，则不需要进行任何防火墙修改。

若要设置每个远程日志记录连接，必须执行以下步骤：

**父进程**

1.  调用 **RemoteLogController：： GenerateConnectionData ( # B1 ** 生成连接数据，这两个进程都必须使用这些数据来启动日志记录连接。

    **注意：** 务必检查此调用的返回值。

    ```cpp
        NoThrowString connectionData;
        Throw::IfFailed(RemoteLogController::GenerateConnectionData(connectionData));

    ```

2.  通过在其环境块中设置连接数据，或通过在命令提示符下将其作为参数传递，来与子进程通信。 例如：

    **在 WexLogger 理解的命令提示符下传递作为命名参数：**  
    /wexlogger \_ connectiondata =* \[ 连接数据 \] *

    **注意：** 如果使用此选项，则**不**需要以下**子进程**部分中的步骤1。

    **作为 WexLogger 理解的命名环境变量传递：**  
    \[YourAppName \_ cmd \] =/wexlogger \_ connectiondata =* \[ 连接数据 \] *

    **注意：** 如果使用此选项，则**不**需要以下**子进程**部分中的步骤1。

    **以任意格式传递到进程 (某个其他命令参数、环境变量等 ) **  
    **注意：** 如果使用此选项，则必须使用以下 **子进程** 部分 **中的步骤** 1。

    **注意：** 为方便起见，"/wexlogger \_ connectiondata =" 值在本机和托管 RemoteLogControllers 中都定义为常量：

    -   **WEX：：日志记录：： c \_ szWexLoggerRemoteConnectionData**，在 LogController 中

    -   **RemoteLogController. WexLoggerRemoteConnectionData**Wex.Logger.Interop.dll

3.  用连接数据启动子进程
4.  调用**RemoteLogController：： InitalizeLogging (* \[ 在步骤 1 \]) 中创建的连接数据* **。 启动子进程后必须进行此调用，因为如果子进程无法及时调用 **LogController：： InitializeLogging ( # B1 ** ，则会超时。

    **注意：** 务必检查此调用的返回值。

    ```cpp
    // ...launch child process with connection data...
    Throw::IfFailed(RemoteLogController::InitializeLogging(connectionData));
    ```

5.  等待子进程，等等。

**子进程**

1.  如果在 WexLogger 了解的命令提示符下，连接数据 **未** 作为命名自变量传递给子进程 (请参阅) 上方的步骤2，则必须设置环境变量，如下所示：

    \[YourAppName \_ cmd \] =/wexlogger \_ connectiondata =* \[ 连接数据 \] *

    例如：

    ```cpp
    // App name is mytestapp.exe
    ::SetEnvironmentVariable(L"mytestapp_cmd", String(c_szWexLoggerRemoteConnectionData).Append(connectionData));
    ```

2.  调用 **LogController：： InitializeLogging ( # B1 ** 为此进程初始化日志记录。 在内部，这将利用上述步骤1中的环境变量集 (或 **父进程** 部分的步骤 2) 来启动返回到父进程的日志记录连接。
3.  日志，等等;所有跟踪都将发送回父进程。
4.  调用 **LogController：： FinalizeLogging ( # B1 ** 来完成此进程的日志记录。

## <a name="determining-test-outcome"></a>确定测试结果


尽管提供了一个方法来显式陈述测试用例的预期结果 (**Log：： Result ( # B2 **) ，但在大多数情况下不 **需要** 使用此方法。

例如，如果测试用例未显式调用 **log：： Result ( # B1 ** **，并且不** 记录错误 (通过 **日志：： error ( # B4 **) ，则默认情况下，它被视为传递测试用例;如果它 **确实** 记录了错误，则测试用例失败。

但是，如果测试用例 **显式调用** **Log：： Result (TestResults：： TestPassed) **，但也 **会** 在测试用例中记录错误，则测试仍将计为失败，因为测试中发生了错误。

在 TAEF 框架中，可以通过使用不同的默认测试结果标记测试来重写此行为。 有关此功能的详细信息可在 "创作 TAEF 测试" 文档中找到。

此行为还可通过以下方式重写：对自己的测试组/测试用例显式调用 **Log：： StartGroup ( # B1 ** ，并使用所选的默认测试结果。

## <a name="generating-wtt-logs"></a>生成 WTT 日志


有三种方法可通过 **WexLogger**生成 WTT 日志。 所有这些都要求 **WttLog.dll** 显示在运行目录或路径中。

-   如果在实验室中运行，安装了 wtt 客户端，将自动为你生成 wtt 日志。 这是因为，WexLogger 会查找两个环境变量是否存在，这些变量仅应存在于实验室环境中： "WttTaskGuid" 和 "WTTRunWorkingDir"。 如果两者都存在，则会自动启用 wtt 日志记录。
-   如果在实验室环境外部的 TAEF 中运行，请在命令提示符下将/enablewttlogging 传递给测试用例。 示例：

    ``` syntax
    te my.test.dll /enablewttlogging
    ```

-   如果要在 TAEF 框架之外使用 WexLogger，但没有在实验室环境中运行，则必须在调用**LogController：： InitializeLogging ( # B1**之前，将** &lt; \_ 进程 \_ 名称 &gt; \_ CMD**环境变量设置为包含此选项。 示例：
    ```cpp
    Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

    ```cpp
    Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/enablewttlogging");
    LogController.InitializeLogging();
    ```

-   如果要将追加到现有的 wtt 日志文件而不是覆盖它，还应同时指定/appendwttlogging 选项和/enablewttlogging.。

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

还可以通过指定以下命令选项之一来完全覆盖或追加到默认 WttLogger 设备字符串：

/WttDeviceString： &lt; 新设备字符串&gt;   
初始化 WttLogger 时，完全重写 WexLogger 使用的 WttDeviceString。

/WttDeviceStringSuffix： &lt; 要追加到设备字符串的值&gt;   
当初始化 WttLogger 时，将指定的值追加到 WexLogger 使用的默认 WttDeviceString。 如果同时指定了 "/WttDeviceString"，则忽略。

下表列出了 WexLogger TestResults 映射到 WttLogger 结果的方式：

| WexLogger | WttLogger                      |
|-----------|--------------------------------|
| Passed    | WTT \_ TESTCASE \_ 结果 \_ 传递    |
| NotRun    | 已 \_ 阻止 WTT TESTCASE \_ 结果 \_ |
| 已跳过   | 已 \_ \_ \_ 跳过 WTT TESTCASE 结果 |
| 已阻止   | 已 \_ 阻止 WTT TESTCASE \_ 结果 \_ |
| 失败    | WTT \_ TESTCASE \_ 结果 \_ 失败    |



## <a name="logger-dependencies"></a>记录器依赖项


本机 c + + 记录器 (**Wex.Logger.dll**) 依赖于 **Wex.Common.dll** 和 **Wex.Communication.dll**。

)  (**Wex.Logger.Interop.dll** 依赖于 **Wex.Logger.dll**、 **Wex.Common.dll** 和 **Wex.Communication.dll**。

此外，当启用 Wtt 日志记录时，需要 **WttLog.dll** 。

## <a name="additional-error-data"></a>其他错误数据


如果记录了错误，则除了错误本身以外，你还可以启用 WexLogger 以包含一个或多个以下项：

-   附带
-   ScreenCapture
-   StackTrace

``` syntax
te my.test.dll /minidumponerror
```

``` syntax
te my.test.dll /screencaptureonerror /stacktraceonerror
```

启用其中一个或多个选项后，每次调用 Log：： Error ( # A1 时都将收到额外的输出。

注意：如果在 TAEF framework 外使用 WexLogger，则必须在调用**LogController：： InitializeLogging ( # B1**之前，将** &lt; \_ 进程 \_ 名称 &gt; \_ CMD**环境变量设置为包含这些选项。 示例：

```cpp
Environment.SetEnvironmentVariable("<YOUR_PROCESS_NAME>_CMD", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

```cpp
Environment.SetEnvironmentVariable("consoleapplication4_cmd", "/screencaptureonerror /minidumponerror /stacktraceonerror");
LogController.InitializeLogging();
```

## <a name="c-error-handling"></a>C + + 错误处理


为了使测试用例作者免于检查每个日志 API 调用的返回值，WexLogger 通过使用可选的回调机制报告意外错误条件; **WexLoggerErrorCallback** 函数。 当 **WexLogger** (通过 **LogController：： InitializeLogging ( # B2 **) 的 initializaiton 时，客户端可以选择指定 **WexLoggerErrorCallback** 函数，以便在 **WexLogger**内发生意外错误情况时调用。 **WexLoggerErrorCallback**函数必须使用以下签名：

```cpp
void __stdcall MyLoggerErrorCallback(const unsigned short* pszMessage, HRESULT hr);
```

WexLoggerErrorCallback 函数的常见用途是将错误消息写出到控制台 (如果你的测试工具是) 的控制台应用程序。 例如，TAEF 框架是 **WexLogger**的客户端，并实现 **WexLoggerErrorCallback** ，这会在出现 WexLogger 错误时将红色文本写入控制台。

## <a name="net-40-compatibility"></a>.NET 4.0 兼容性


Wex 编译为 NetFx 2/3/3.5 二进制文件，以便可将其加载到 NetFx 2/3/3.5 和 NetFx 4 进程中。 这允许 TAEF 运行 NetFx 2 以上的所有托管程序集。 如果在 TAEF 外使用 Wex，则需要为 exe 添加一个配置 [文件](/previous-versions/visualstudio/visual-studio-2008/ms229689(v=vs.90)) ，以配置 NetFx 4 运行时，以将 NetFx 2/3/3.5 二进制文件加载到其进程中。 配置文件应包含以下内容：

```cpp
<configuration> 
    <startup useLegacyV2RuntimeActivationPolicy="true">
        <supportedRuntime version="v4.0"/>
    </startup>
</configuration>
```

## <a name="managed-code-error-and-exception-handling"></a>托管代码错误和异常处理


为了使测试用例作者免于检查每个 **日志** API 调用的返回值，WexLogger 的托管层通过使用 **LoggerController. WexLoggerError** 事件报告意外的错误条件。 可以通过实现自己的 **WexLoggerErrorEventHandler** 并使用以下 c # 事件订阅的熟悉语法，随时订阅此事件：

```cpp
LogController.WexLoggerError += new WexLoggerEventHandler(My_WexLoggerErrorHandler);
```

下面是事件处理程序的示例：

```cpp
static void LogController_WexLoggerError(object sender, WexLoggerErrorEventArgs e)
{
    ConsoleColor originalColor = Console.ForegroundColor;
    Console.ForegroundColor = ConsoleColor.Red;
    Console.WriteLine("LogController_WexLoggerError: " + e.Message);
    Console.ForegroundColor = originalColor;
}
```

此外，当发生故障时， **LogController：： InitializeLogging ( # B1 ** 和 **LogController：： FinalizeLogging ( # B3 ** 方法本身引发 WexLoggerException。 这提供了有关错误的详细信息，并且还允许您在测试运行开始之前将其中止。 测试用例作者永远无需担心这些例外，只应在 WexLogger initializaiton/完成期间进行预期/处理。