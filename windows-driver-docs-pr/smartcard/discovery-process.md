---
title: 发现过程
description: 发现过程
ms.assetid: 6B94CAF1-D998-4EAF-8ABB-80A21193B50F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387156e207d49778358e332ecfccc29551dab5ff
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716856"
---
# <a name="discovery-process"></a>发现过程


从 Windows 7 开始，通过 Windows 徽标计划 (WLP) 的徽标认证的智能卡微型驱动程序由 Windows 即插即用组件自动下载和安装。 Windows 7 还介绍了一类微型驱动程序，适用于 PIV 兼容的卡和支持 GID 卡边缘的卡。

将智能卡插入读卡器后，Windows 会执行以下发现过程：

-   智能卡即插即用过程：

    此过程请求并下载通过即插即用 Windows 更新的徽标认证微型驱动程序。

-   Winscard 发现进程：

    此过程将兼容的智能卡与与 PIV 或 GID 兼容的类微型驱动程序相关联。

-   Windows 智能卡类微型驱动程序发现过程：

    此过程将安装的微型驱动程序与智能卡相关联。

下表列出了不同发现进程使用的辅助值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">帮助名称</th>
<th align="left">帮助值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">PIV 帮助</td>
<td align="left">A0 00 00 03 08 00 00 10 00 xx yy</td>
<td align="left">PIV 帮助，不包含版本信息。 Microsoft 智能卡框架忽略最小有效2个字节。</td>
</tr>
<tr class="even">
<td align="left">MS GID 辅助</td>
<td align="left">A0 00 00 03 97 42 54 46 59 xx yy</td>
<td align="left"><p>Microsoft (MS) GID 帮助，其中不包括版本信息。</p>
<p>最小有效2字节不会发送到卡，而是由主机保留，如下所示：</p>
<ul>
<li>其中的第一个字节 (xx) 用于 GID 版本号的 Windows 智能卡框架。 此字节必须设置为 GID 或0x02 的 GID 规范修订号。</li>
<li>第二个字节 (yy) 保留供卡片应用程序使用。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">SC PNP 辅助</td>
<td align="left">A0 00 00 03 97 43 49 44 5F 01 00</td>
<td align="left">智能卡即插即用辅助。</td>
</tr>
</tbody>
</table>

 

下表列出了发现过程使用的文件。

| Command | 指令 () 值 |
|---------|-------------------------|
| MF      | 0x3F00                  |
| EF.ATR  | 0x2F01                  |

 

下表列出了不同的发现进程使用的命令。

| Command      | 指令 () 值 |
|--------------|-------------------------|
| SELECT       | 0xA4                    |
| 获取数据     | 0xCA                    |
| 获取响应 | 0xC0                    |

 

## <a name="span-idsmart_card_plug_and_play_processspanspan-idsmart_card_plug_and_play_processspanspan-idsmart_card_plug_and_play_processspansmart-card-plug-and-play-process"></a><span id="Smart_Card_Plug_and_Play_Process"></span><span id="smart_card_plug_and_play_process"></span><span id="SMART_CARD_PLUG_AND_PLAY_PROCESS"></span>智能卡即插即用进程


如果没有可用的兼容收件箱微型驱动程序，即插即用安装智能卡微型驱动程序。 即插即用还会通过 Windows 更新更新已安装的智能卡微型驱动程序。

若要执行这些任务，即插即用必须能够为智能卡派生唯一的 ID。 从 Windows 7 开始，下面介绍了即插即用使用来派生卡的唯一 ID 的智能卡发现过程：

1.  即插即用从 ATR 获取历史字节。 这些字节稍后会在此发现过程中使用。
2.  即插即用发出选择命令以查找 SC PNP 辅助工具。即插即用发出 "获取数据" 命令，以查找 Windows 专用标记 0x7F68 (") 的" "。 有关详细信息，请参阅以下子节 "Windows 智能卡框架卡标识符"。 如果此命令成功，将返回唯一标识符的列表。 即插即用使用列表中的第一个标识符作为智能卡的设备 ID，并使用此值作为卡的唯一 ID。 有关详细信息，请参阅 [设备 id](../install/device-ids.md)。
3.  如果即插即用为智能卡派生了唯一 ID，则会继续执行步骤12。
4.  如果 Windows 无法在上述步骤中获取设备 ID，则会发出一个 MF 和 EF 的选择。ATR 后跟读取二进制命令，如果 Windows 成功获取了可用作 WU 设备 ID 的唯一标识符，请访问步骤12。
5.  如果即插即用无法获取上述步骤中的唯一标识符，则会发出 PIV 辅助工具的选择命令。 如果即插即用成功，则会将智能卡视为与 PIV 兼容的设备。 即插即用使用以下内容作为卡的唯一 ID：

    1.  与设备兼容的 ID 的 PIV 兼容设备 ID。 有关详细信息，请参阅 [兼容 id](../install/compatible-ids.md)。
    2.  智能卡的 ATR 历史字节作为设备 ID。 如果没有历史 ATR 字节，则 Windows 将使用 PIV 兼容的设备 id 作为设备 ID。

6.  如果即插即用为智能卡派生了唯一 ID，则会继续执行步骤12。
7.  如果步骤4中的 SELECT 命令未成功，Windows 将发出 MS GID 辅助工具的选择命令。如果即插即用选择 MS GID 辅助工具，它会将智能卡视为与 GID 兼容的设备。 即插即用使用以下内容作为卡的唯一 ID：

    1.  与 GID 兼容的设备 ID 作为兼容 ID。
    2.  智能卡的 ATR 历史字节作为设备 ID。 如果没有历史 ATR 字节，即插即用会使用与 GID 兼容的设备 ID 作为设备 ID。

8.  如果即插即用为智能卡派生了唯一 ID，则会继续执行步骤12。
9.  如果即插即用无法选择 PIV 辅助工具或 MS GID 辅助工具，它将使用卡的 ATR 历史 (字节，如果有任何) 作为智能卡唯一 ID 的设备 ID。
10. 如果即插即用没有 ATR 历史字节，则没有足够的 Windows 更新信息。 即插即用无法通过放弃 E 意外发现过程失败 \_ \_ 。
11. 如果即插即用为智能卡派生了唯一 ID，则会继续执行步骤12。
12. 即插即用停止发现过程，并使用唯一标识符。

从 fromWindows 8 开始，如果即插即用找不到卡的驱动程序，卡将与收件箱 NULL 驱动程序配对。 在连接到连接到 PC 的智能卡读卡器时，该卡需要其他特定于卡的软件才能正常工作。

## <a name="span-idwinscard_discovery_processspanspan-idwinscard_discovery_processspanspan-idwinscard_discovery_processspanwinscard-discovery-process"></a><span id="Winscard_Discovery_Process"></span><span id="winscard_discovery_process"></span><span id="WINSCARD_DISCOVERY_PROCESS"></span>Winscard 发现过程


Winscard ( # A0) 发现进程用于将系统中的卡片与安装的微型驱动程序相关联。 调用 [**SCardListCards**](/windows/win32/api/winscard/nf-winscard-scardlistcardsa) 或 [**SCardLocateCards**](/windows/win32/api/winscard/nf-winscard-scardlocatecardsa) 时，将启动进程。

从 Windows 7 开始，下面介绍了 Winscard 发现过程：

1.  Winscard 会在注册表中查找表示计算机上安装的智能卡的各种子项的 Calais 项。 这些子项位于：

    HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ 加密 \\ Calais \\ 智能卡

2.  Winscard 搜索智能卡子项下的每个子项，以获得子项的 ATR 值与从智能卡获取的 ATR 值之间的匹配项。 如果找到匹配项，请跳到步骤6。
3.  Winscard 查找微型驱动程序的智能卡子项值与 PIV IDMP 的 PIV 设备 ATR Cache (中的值之间的匹配项，) 或 ATR Cache (for Microsoft GID 兼容的卡) 子项。 如果找到匹配项，请跳到步骤6。
4.  Winscard 发出 MS GID 辅助工具的选择命令。 如果此命令成功，请跳到步骤6。
5.  如果步骤4失败，Winscard 将发出 PIV 辅助工具的选择命令。 如果此命令成功，请跳到步骤6。
6.  Winscard 返回卡的名称，该名称对应于与卡匹配的微型驱动程序注册表项。

**注意**   下表描述了 Winscard 发现进程使用的各种注册表项。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表项</th>
<th align="left">使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \Cryptography\Calais\SmartCards</td>
<td align="left">Winscard 在步骤1中使用此密钥作为 Calais\SmartCards 键。</td>
</tr>
<tr class="even">
<td align="left">HKEY_LOCAL_MACHINE \ SOFTWARE\Microsoft \Cryptography\Calais\PIV 设备 ATR 缓存</td>
<td align="left"><p>如果在步骤4中找到匹配项，则匹配卡的完整 ATR 将作为二进制值存储在此注册表项中。 该项的名称是随机选择的。</p>
<p>缓存此项后，在步骤3中使用它来提高性能。</p></td>
</tr>
<tr class="odd">
<td align="left">HKEY_LOCAL_MACHINE \ SOFTWARE\Microsoft \Cryptography\Calais\IDMP ATR 缓存</td>
<td align="left"><p>如果在步骤5中找到了匹配项，则匹配卡的完整 ATR 将以二进制值的形式存储在此注册表项下。 该项的名称是随机选择的。</p>
<p>缓存此项后，在步骤3中使用它来提高性能。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-id_windows_smart_card_class_minidriver_discovery_processspanspan-id_windows_smart_card_class_minidriver_discovery_processspanspan-id_windows_smart_card_class_minidriver_discovery_processspan-windows-smart-card-class-minidriver-discovery-process"></a><span id="_Windows_Smart_Card_Class_Minidriver_Discovery_Process"></span><span id="_windows_smart_card_class_minidriver_discovery_process"></span><span id="_WINDOWS_SMART_CARD_CLASS_MINIDRIVER_DISCOVERY_PROCESS"></span> Windows 智能卡类微型驱动程序发现过程


调用 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85)) 时，Windows 智能卡类微型驱动程序执行以下发现过程。 微型驱动程序执行此发现过程以将关联的卡标记为 PIV 或 Microsoft GID 兼容：

1.  微型驱动程序发出 PIV 辅助工具的选择命令。 如果此命令成功，则该卡会被标记为 PIV 兼容，发现过程将停止。
2.  否则，微型驱动程序会发出 MS GID 辅助工具的选择命令。 如果命令成功或找不到帮助，则微型驱动程序会将卡标记为 MS GID。

**注意**  
-   如果以前通过微型驱动程序类的 Winscard 发现过程发现了智能卡，则它可能无法响应 PIV 或 GID 辅助工具的 SELECT 命令。 在这种情况下，它必须是供应商提供的卡，它使用自定义辅助工具实现 GID 卡边缘。 此类卡可以通过其他数据对象来扩展 Microsoft 智能卡数据模型。
-   PIV 和 GID 智能卡供应商可以使用 Windows 智能卡类微型驱动程序，并通过提供仅 INF 安装包来添加品牌。 有关对兼容卡使用类微型驱动程序的详细信息，请参阅 [智能卡即插即用](smart-card-plug-and-play.md)中的 INF 示例。 只有历史字节用于 INF 中的即插即用匹配。

    供应商提供的 INF 文件在 Calais \\ 智能卡注册表子项下创建包含以下信息的条目。

    | 条目名称                      | 类型   | 值                                     |
    |---------------------------------|--------|-------------------------------------------|
    | 80000001                        | String | Msclmd.dll                                |
    | ATR                             | 二进制 | 卡片的 ATR                                |
    | ATRMask                         | 二进制 | 卡片的 ATR 掩码                           |
    | 加密提供程序                 | String | Microsoft Base Smart Card Crypto Provider |
    | 智能卡密钥存储提供程序 | String | Microsoft 智能卡密钥存储提供程序 |

     

 

## <a name="span-idselection_mechanismsspanspan-idselection_mechanismsspanspan-idselection_mechanismsspanselection-mechanisms"></a><span id="Selection_Mechanisms"></span><span id="selection_mechanisms"></span><span id="SELECTION_MECHANISMS"></span>选择机制


### <a name="span-idapplications_that_contain_microsoft_identifiersspanspan-idapplications_that_contain_microsoft_identifiersspanspan-idapplications_that_contain_microsoft_identifiersspanapplications-that-contain-microsoft-identifiers"></a><span id="Applications_that_Contain_Microsoft_identifiers"></span><span id="applications_that_contain_microsoft_identifiers"></span><span id="APPLICATIONS_THAT_CONTAIN_MICROSOFT_IDENTIFIERS"></span>包含 Microsoft 标识符的应用程序

Windows 智能卡框架尝试使用 Microsoft 即插即用辅助工具来选择应用程序。 如果卡不支持指定的辅助功能，则它应在 SELECT 命令后返回错误。 如果 SELECT 命令成功完成，则框架将尝试通过发出 "获取数据" 命令来识别卡和对应的智能卡微型驱动程序。

不管是否支持 SC 即插即用辅导，都将发生 "获取数据" 命令。 这允许应用程序（这些应用程序要么与其他帮助相关联，要么与任何帮助都不关联）都可以实现此规范中的卡选择机制。

### <a name="span-id_get_dataspanspan-id_get_dataspan-get-data"></a><span id="_GET_DATA"></span><span id="_get_data"></span> 获取数据

在卡上选择即插即用 MS 辅助工具后，智能卡框架将发出带有 Windows 专用标记0x7F68 的 "获取数据" 命令。 如果卡支持 "获取数据" 命令和专用标记，它将返回一个或多个唯一标识符的列表。 必须按照以下 "Windows 智能卡框架卡标识符" 部分的定义来构造唯一标识符。

Windows 智能卡框架只使用列表中的第一个唯一标识符来查找并安装适当的智能卡微型驱动程序。 将来可以使用其他标识符。

### <a name="span-id_select_piv_aid_commandspanspan-id_select_piv_aid_commandspanspan-id_select_piv_aid_commandspan-select-piv-aid-command"></a><span id="_SELECT_PIV_AID_Command"></span><span id="_select_piv_aid_command"></span><span id="_SELECT_PIV_AID_COMMAND"></span> 选择 PIV 辅导命令

为了识别 PIV 应用程序，Windows 将发出 SELECT PIV 辅助命令。 如果此命令成功，则表示 PIV 应用程序出现在卡上，并且现在处于选中状态。 在这种情况下，Windows 智能卡框架现在可以将符合 PIV 标准的微型驱动程序与卡关联起来。

### <a name="span-id_select_ms_gids_aid_commandspanspan-id_select_ms_gids_aid_commandspanspan-id_select_ms_gids_aid_commandspan-select-ms-gids-aid-command"></a><span id="_SELECT_MS_GIDS_AID_Command"></span><span id="_select_ms_gids_aid_command"></span><span id="_SELECT_MS_GIDS_AID_COMMAND"></span> 选择 MS GID 辅助命令

若要确定 MS GID 应用程序，请使用 SELECT MS GID 辅助命令。 如果此命令成功，则会在卡上出现 MS GID 应用程序，并且该应用程序现在处于选中状态。 现在，Windows 智能卡框架可以将与 MS GID 兼容的微型驱动程序与卡关联起来。

### <a name="span-iduse_of_the_atr_historical_bytesspanspan-iduse_of_the_atr_historical_bytesspanspan-iduse_of_the_atr_historical_bytesspanuse-of-the-atr-historical-bytes"></a><span id="Use_of_the_ATR_Historical_Bytes"></span><span id="use_of_the_atr_historical_bytes"></span><span id="USE_OF_THE_ATR_HISTORICAL_BYTES"></span>使用 ATR 历史字节数

在以下条件下，Windows 智能卡框架将恢复为使用 ATR 历史字节 ATR 来确定要加载的微型驱动程序：

-   智能卡不支持 "获取数据" 命令。
-   智能卡不支持此规范中的辅助选择方法。

使用 ATR 历史字节是用于标识插入的卡片的旧方法。 框架在搜索微型驱动程序时使用所有历史字节。

### <a name="span-id_windows_smart_card_framework_card_identifierspanspan-id_windows_smart_card_framework_card_identifierspanspan-id_windows_smart_card_framework_card_identifierspan-windows-smart-card-framework-card-identifier"></a><span id="_Windows_Smart_Card_Framework_Card_Identifier"></span><span id="_windows_smart_card_framework_card_identifier"></span><span id="_WINDOWS_SMART_CARD_FRAMEWORK_CARD_IDENTIFIER"></span> Windows 智能卡框架卡标识符

如果智能卡支持 "获取数据" 命令，则 Windows 智能卡框架会要求卡返回一个以以下的第1个

``` syntax
CardID ::= SEQUENCE {
                   version Version DEFAULT v1,
                   vendor VENDOR,
                   guids GUIDS }

Version ::= INTEGER {v1(0), v2(1), v3(2)}
VENDOR ::= IA5STRING(SIZE(0..8))
GUID ::= OCTET STRING(SIZE(16))
GUIDS ::= SEQUENCE OF GUID
```

版本成员必须设置为 0 (v1) 。

供应商成员必须设置为 "MSFT"。

GUID 成员是一个16字节的 GUID，用于唯一标识智能卡/应用程序组合。 此值用于检测和加载适当的智能卡微型驱动程序。

**注意**   颁发应用程序的 IHV 或 ISV 必须为其卡/应用程序组合创建唯一的 GUID。

 

 

