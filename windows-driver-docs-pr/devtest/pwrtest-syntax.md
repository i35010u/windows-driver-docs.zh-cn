---
title: PwrTest 语法
description: 从命令提示符窗口运行 PwrTest。 可以选择并配置 PwrTest 方案使用命令选项。
ms.assetid: bcae1bb6-ce5b-4ece-a5ba-bae6fefd6408
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11fcadb173c449473e7827d536b8cc7c82e60ca2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525534"
---
# <a name="pwrtest-syntax"></a>PwrTest 语法


从命令提示符窗口运行 PwrTest。 可以选择和配置[PwrTest 方案](pwrtest-scenarios.md)使用命令选项。

PwrTest 工具的语法是：

```
pwrtest /scenario [/scenario_options] [/common_options]
```

<span id="_scenario"></span><span id="_SCENARIO"></span>**/**<em>scenario</em>  

| 方案   | 描述                                                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sleep       | 周期睡眠/恢复转换通过计算机。 (Windows 7 及更高版本)                                                                                        |
| 电池     | 提供了电池信息和监视。 (Windows 7 及更高版本)                                                                                                 |
| 信息        | 提供系统电源的信息。 (Windows 7 及更高版本)                                                                                                           |
| 是          | 监视器的线程执行状态。 (Windows 7 及更高版本)                                                                                                             |
| 空闲        | 监视系统空闲事件。 (Windows 7 及更高版本)                                                                                                                 |
| ppm         | 监视处理器电源管理。 (Windows 7 及更高版本)                                                                                                         |
| 计时器       | 监视系统计时器分辨率更改。 (Windows 7 及更高版本)                                                                                                    |
| 磁盘        | 监视磁盘空闲的统计信息和向下数值调节钮的事件。 (Windows 7 及更高版本)                                                                                          |
| 设备      | 监视设备空闲统计信息和电源关闭事件。 (Windows 7 及更高版本)                                                                                       |
| 监视器     | 记录用户空闲统计信息与监视器/显示自动变暗和消隐功能相关。(Windows 7 及更高版本)                                                            |
| requests    | 显示未完成的和新功能请求。 (Windows 7 及更高版本)                                                                                                 |
| 温度     | 监视器 ACPI 温度区信息和统计信息。 报告过热区域和温度变化的系统上仅支持此功能。 (Windows 7 及更高版本)。 |
| processidle | 强制后台维护任务执行 （现在而非在其计划的时间），将监视其进度。 (Windows 7 及更高版本)                        |
| cs          | 如果系统支持，周期经过连接备用转换的计算机。 (Windows 8 及更高版本)                                               |
| platidle    | 监视并尝试登录平台空闲转换计数，如果系统支持。 (Windows 8 及更高版本)                                            |
 

 


<span id="_scenario_options"></span><span id="_SCENARIO_OPTIONS"></span>**/**<em>scenario\_options</em>  
若要查看可用于每个 Pwrtest 方案的选项，请键入： **pwrtest.exe /**<em>方案</em> **/？**

例如： **pwrtest.exe /sleep /？**

<span id="_common_options"></span><span id="_COMMON_OPTIONS"></span>/*common\_options*  

|       *common\_options*       |                                                                                                                描述                                                                                                                 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **/lf:**<em>文件夹</em>    |                                            指定日志文件的文件夹。 例如，c:\\myfolder 或\\ \\server\\共享。 默认日志位置是 pwrtest.exe 所在的文件夹。                                             |
|     **/ln:**<em>name</em>     |                指定日志文件的名称和事件跟踪 Windows (ETW) 跟踪会话的名称。 （.wtl、.xml 等），将自动添加日志文件扩展名。 默认名称为 pwrtestlog。                |
| **/etwbuffersize:**<em>n</em> |                                                  如果此值大于默认大小以 kb 为单位指定 ETW 缓冲区大小。 默认值为当前页大小或 256 KB （两者中较大）。                                                  |
| **/etwminbuffers:**<em>n</em> |                                指定最小为 ETW 会话 2 每个逻辑处理器的最小值大于分配的缓冲区数。 默认值为每个逻辑处理器的 2 个缓冲区。                                |
| **/etwmaxbuffers:**<em>n</em> | 指定的最大数量的缓冲区分配的 ETW 会话，如果该数字大于 2 每个逻辑处理器的最小值和大于**etwminbuffers**设置。 默认值是**etwminbuffers**值 + 20。 |
|        **/delaywrite**        |                                                           指定日志数据进行缓冲处理的内存来减少写入磁盘中。 此选项会影响所有日志类型包括 ETL。                                                            |

**示例**

```
pwrtest /?  
```

```
pwrtest /requests  /?
```

```
pwrtest /requests  /t:60
```

### <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注

若要支持 ETW 跟踪的执行要求：

-   必须从管理员或提升运行 Pwrtest**命令提示符**窗口 (**以管理员身份运行**)。

-   Pwrtest 必须以本机方式运行 (不支持 WoW64)。

实施相应的系统管理员的组策略设置可能会影响某些情况下，需要临时修改电源设置值 （如睡眠方案中）。

PwrTest 在.log （明文） 中自动生成每次执行多个日志.xml （格式因方案），.wtl (WTTLog) 和.etl （ETW 跟踪） 日志格式。

若要能够使用所有 PwrTest 方案，必须先设置测试计算机以用于使用 Visual Studio 和 WDK 测试。 有关详细信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)，或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)。 某些情况下需要是一部分的 Windows 驱动程序测试框架 (WDTF) 的电源按钮驱动程序。 预配的系统，使用 Visual Studio 和 WDK 测试时，会自动安装 WDTF （和包含的电源按钮驱动程序）。 WDTF 有关的信息，请参阅[ **Windows 设备测试框架 (WDTF) （Windows 驱动程序）**](https://msdn.microsoft.com/library/windows/hardware/ff539547)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[PwrTest 方案](pwrtest-scenarios.md)

[PwrTest 日志文件](pwrtest-log-file.md)

 

 






