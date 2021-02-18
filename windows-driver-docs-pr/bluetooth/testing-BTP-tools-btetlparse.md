---
title: Microsoft 蓝牙测试平台-BTETLParse
description: 蓝牙测试平台 (BTP) 蓝牙 ETL 分析。
ms.date: 1/12/2021
ms.localizationpriority: medium
ms.openlocfilehash: 310a673b410dc2717ae176a120e420e9d91fa917
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648100"
---
# <a name="bluetooth-etl-parse-btetlparseexe"></a>蓝牙 ETL 分析 (BTETLParse.exe) 

蓝牙 ETL 分析工具从包含压缩蓝牙数据的 ETL 文件中提取 HCI 跟踪。

此工具旨在分析使用 [GitHub 上的 Windows](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md)存储库的总线工具收集的 ETL 文件。

[Tracefmt](../devtest/tracefmt.md) 是一种方法，用于分析 ETL 文件中的其他日志。

## <a name="etl-parse-command-line-options"></a>ETL 分析命令行选项

```console
Usage: btetlparse [-cfa <output_cfa_filename>] [-hci <output_hci_filename>]
[-pcap <output_pcap_filename>] [-pcapng <output_pcapng_filename>]
[<input_etl_filename>] [<additional_input_etl_filenames>]

    -cfa through -pcapng flags parse the etl file into different file types.

    -cfa <filename>         Data file readable by Frontline protocol analyzers.

    -hci <filename>         Data file in plain text format.

    -pcap <filename>        Data file readable by Wireshark protocol analyzers.
        
    -pcapng <filename>      Data file readable by Wireshark protocol analyzers.

    <input_etl_filename>    The is the filename of the ETL file we are trying to parse.
                                Default is c:\temp\btetw.etl

    <additional_input_etl_filenames>    BTETLParse can parse multiple ETL files at a time.
```

## <a name="etl-parse-usage-example"></a>ETL 分析用法示例

将 [适用于 GitHub 上的 Windows](https://github.com/microsoft/busiotools/blob/master/bluetooth/tracing/readme.md) 存储库的总线工具收集的 ETL 文件移动到与提取的 BTP 包中的 BTETLParse 相同的文件夹中。 然后运行：

- `btetlparse -cfa BthTracing.cfa -hci BthTracing.hci -pcap BthTracing.pcap -pcapng BthTracing.pcapng BthTracing.etl` 从命令提示符/PowerShell 控制台

此命令分析 `BthTracing.etl` 所有可用的文件类型。 有关每个文件类型的说明，请参阅上面的命令行选项。