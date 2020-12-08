---
title: IRP 日志记录
description: 驱动程序验证程序的 IRP 日志记录功能监视驱动程序使用的 Irp，并记录 IRP 的使用情况。 此记录以 WMI 信息形式存储。
keywords:
- IRP 日志记录功能 WDK 驱动程序验证程序
- DC2WMIParser 工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81b46763bfd1aa6f4d28ae8064b969d5daaa4c11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838631"
---
# <a name="irp-logging"></a>IRP 日志记录


驱动程序验证程序的 IRP 日志记录功能监视驱动程序使用的 Irp，并记录 IRP 的使用情况。 此记录以 WMI 信息形式存储。

## <span id="ddk_irp_logging_tools"></span><span id="DDK_IRP_LOGGING_TOOLS"></span>


Windows 驱动程序工具包 (WDK) 包含工具)  ( DC2WMIParser，该工具可将此 WMI 记录转换为文本文件。

此驱动程序验证程序选项仅在 Windows Server 2003 及更高版本中可用。

### <a name="span-idthe_wmi_recordspanspan-idthe_wmi_recordspanthe-wmi-record"></a><span id="the_wmi_record"></span><span id="THE_WMI_RECORD"></span>WMI 记录

对于每个设备，WMI 记录将不包含20个以上的 Irp。 记录第二十五次 IRP 后，将替换第一个 IRP 记录。 因此，如果记录列出二十个 Irp，则这些 Irp 始终是最新的，但没有办法知道哪一个是最新的。

由于 WMI 记录存储在内存中，因此在计算机重新启动时，会将其清除。 因此，请使用 DC2WMIParser 将此信息保存到文件。

如果使用 **/t** 选项，DC2WMIParser 将在指定的持续时间内连续运行。 在这种情况下，每个采样期间，记录可以包含20个以上的 Irp (多达20个 irp) 。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 IRP 日志记录功能。

若要激活 IRP 日志记录功能，还必须激活 [I/o 验证](i-o-verification.md)。

-   **在命令行中**

    在命令行中，IRP 日志记录选项由 **0x400** (位 10) 表示。

    若要激活 IRP 日志记录，请使用0x410 的标志值或将0x410 添加到标志值。 此值 (0x10) 和 IRP 日志记录 (0x400) 激活 [I/o 验证](i-o-verification.md) 。 例如：

    ```
    verifier /flags 0x410 /driver MyDriver.sys
    ```

    此功能将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，来激活和停用 IRP 日志记录，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x410 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

-   **使用驱动程序验证器管理器**
    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")** ，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 (检查) **IRP 日志记录** 和 [i/o 验证](i-o-verification.md)。

### <a name="span-iddc2wmiparserspanspan-iddc2wmiparserspandc2wmiparser"></a><span id="dc2wmiparser"></span><span id="DC2WMIPARSER"></span>DC2WMIParser

DC2WMIParser 是一种工具，用于收集驱动程序验证器创建的 WMI IRP 记录，并将此日志转换为文本文件。

DC2WMIParser 语法如下所示：

```
dc2wmiparser [/f File] [/t Time]
```

这些参数具有以下含义：

<span id="_________fFile"></span><span id="_________ffile"></span><span id="_________FFILE"></span>**/F**_文件_  
指定要写入的日志文件的完整路径和文件名。 相对于当前目录，将采用相对路径。 如果省略此项，则将使用当前目录中的文件名 dc2verifier。

<span id="_tTime"></span><span id="_ttime"></span><span id="_TTIME"></span>**/T**_时间_  
指定 DC2WMIParser 将继续运行的时间长度（以分钟为单位）。 如果 *Time* 等于零，DC2WMIParser 将记录已由驱动程序验证程序存储的所有 WMI IRP 信息，然后退出。 如果将 *Time* 设置为正值，则在指定的时间长度 DC2WMIParser 将继续运行，并在新信息到达时存储新信息。 默认值为零。

### <a name="span-idformat_of_dc2wmiparser_log_filesspanspan-idformat_of_dc2wmiparser_log_filesspanformat-of-dc2wmiparser-log-files"></a><span id="format_of_dc2wmiparser_log_files"></span><span id="FORMAT_OF_DC2WMIPARSER_LOG_FILES"></span>DC2WMIParser 日志文件的格式

DC2WMIParser 生成的文件是一个 ASCII 文本文件。

此文件的第一行包含一个小数值，表示文件中记录的设备数。

在第一行之后，该文件分成几个部分;每个部分介绍一种设备。

对于每个设备，格式为：

-   **在一行上：** 设备名称。

-   **在一行上：** 指定此设备的设备类型和函数的数量的小数。

-   **对于每种设备类型和函数在一行上：** 三个十六进制数字，用逗号分隔。 这表示设备类型以及在此记录中记录的最低和最高函数。

-   **在每个设备类型和功能的一组行中：**
    -   单行，其十进制数字用于指定当前设备类型的 IOCTLs 的计数。
    -   对于每个 IOCTL，都有一行。 其中每一行都包含六个用逗号分隔的十六进制数字。 这些指定设备类型、函数、方法、访问、输入缓冲区的长度和输出缓冲区的长度。

下面是一个 DC2WMIParser 日志文件示例。 在实际文件中，不会有任何空格、注释或空白行，但这些行已添加到此示例中以使其更清晰。

```
2           There are two devices described by this log file.

The first device begins here:

  DP(1)0x7e00-0x21dbda400+3   Device name of the first device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420

    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0

The second device begins here:

  DP(1)0x7e00-0x21dbda400+2   Device name of the second device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420


    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0
```

 

 





