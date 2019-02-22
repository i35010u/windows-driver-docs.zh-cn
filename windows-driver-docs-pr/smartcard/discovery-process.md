---
title: 发现过程
description: 发现过程
ms.assetid: 6B94CAF1-D998-4EAF-8ABB-80A21193B50F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8906f30a46eff14f77d13550247ab845328a007
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544336"
---
# <a name="discovery-process"></a>发现过程


从 Windows 7 开始，智能卡微型驱动程序的徽标认证通过 Windows 徽标计划 (WLP) 会自动下载和安装的 Windows 即插即用和播放组件。 Windows 7 还引入了类的 PIV 兼容卡微型驱动程序和支持 GID 卡卡边缘。

智能卡插入到读取器中，Windows 将执行以下的发现进程：

-   智能卡即插过程：

    此过程请求，并通过插从 Windows 更新下载徽标认证的微型驱动程序。

-   Winscard 发现过程：

    此过程将兼容的智能卡与 PIV 或 GID 兼容类微型驱动程序相关联。

-   Windows 智能卡类微型驱动程序发现过程：

    此过程将安装微型驱动程序与智能卡相关联。

下表列出了不同的发现进程使用的辅助设备值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">辅助工具名称</th>
<th align="left">辅助值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">PIV 辅助设备</td>
<td align="left">A0 00 00 03 08 00 00 10 00 xx yy</td>
<td align="left">PIV 辅助设备，它不包含版本信息。 Microsoft 智能卡框架将忽略最低有效的 2 个字节。</td>
</tr>
<tr class="even">
<td align="left">MS GID 帮助</td>
<td align="left">A0 00 00 03 97 42 54 46 59 xx yy</td>
<td align="left"><p>Microsoft (MS) GID 辅助设备，它不包含版本信息。</p>
<p>最低有效的 2 个字节不会发送到卡中，但保留了主机，如下所示：</p>
<ul>
<li>GID 版本号，这两个字节 (xx) 的第一个可供 Windows 智能卡框架。 此字节必须设置为 GID 规范修订号即 0x01 或 0x02。</li>
<li>卡应用程序的情况下，第二个字节 (yy) 保留供使用。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">SC 即插即用辅助设备</td>
<td align="left">A0 00 00 03 97 43 49 44 5F 01 00</td>
<td align="left">智能卡插辅助工具。</td>
</tr>
</tbody>
</table>

 

下表列出了由发现过程所使用的文件。

| 命令 | 指令 (INS) 值 |
|---------|-------------------------|
| MF      | 0x3F00                  |
| EF.ATR  | 0x2F01                  |

 

下表列出了不同的发现进程使用的命令。

| 命令      | 指令 (INS) 值 |
|--------------|-------------------------|
| 选择       | 0xA4                    |
| 获取数据     | 0xCA                    |
| 获取响应 | 0xC0                    |

 

## <a name="span-idsmartcardplugandplayprocessspanspan-idsmartcardplugandplayprocessspanspan-idsmartcardplugandplayprocessspansmart-card-plug-and-play-process"></a><span id="Smart_Card_Plug_and_Play_Process"></span><span id="smart_card_plug_and_play_process"></span><span id="SMART_CARD_PLUG_AND_PLAY_PROCESS"></span>智能卡即插过程


Plug and Play 安装智能卡微型驱动程序不兼容的收件箱微型驱动程序是否可用。 插还会更新已安装的智能卡微型驱动程序通过 Windows 更新。

若要执行这些任务之一，插必须能够派生智能卡的唯一 ID。 从 Windows 7 开始，下面介绍的智能卡发现过程插即用来派生卡片的唯一 ID:

1.  插从 ATR 获取历史的字节数。 此发现过程中更高版本使用这两个字节。
2.  插发出 SELECT 命令来查找 SC 即插即用辅助设备。Plug and Play 获取数据命令，以找到 Windows 专有标记 0x7F68 （按 ASN.1 der 方式编码的） 问题。 有关详细信息，请参阅"Windows 智能卡框架卡标识符"下一节。 如果此命令成功，则返回的唯一标识符的列表。 插智能卡的设备 ID 作为使用列表中的第一个标识符并使用该值的卡的唯一 id。 有关详细信息，请参阅[设备 Id](https://msdn.microsoft.com/library/windows/hardware/ff541237)。
3.  如果插派生而来的智能卡的唯一 ID，它将继续到步骤 12。
4.  如果 Windows 无法获取设备 ID 在前面步骤中的，它将发出 MF 和 EF 的选择。如果 Windows 成功获取它可以使用 WU 作为设备 ID 的唯一标识符后跟的二进制读取命令的 ATR 转到步骤 12。
5.  如果插无法获取在前面步骤中的唯一标识符，它为 PIV 辅助设备发出 SELECT 命令。 如果插成功，将其视为智能卡 PIV 兼容设备。 插使用智能卡的唯一 ID 作为以下：

    1.  PIV 兼容设备 ID 作为设备的兼容 id。 有关详细信息，请参阅[兼容 Id](https://msdn.microsoft.com/library/windows/hardware/ff539950)。
    2.  卡片的 ATR 历史个字节作为设备 id。 如果不有任何历史 ATR 字节，Windows 将使用 PIV 兼容设备 id 作为设备 id。

6.  如果插派生而来的智能卡的唯一 ID，它将继续到步骤 12。
7.  如果在步骤 4 中选择的命令失败，Windows 为 MS GID 辅助设备发出 SELECT 命令。如果选择 MS GID 帮助插成功，将其视为智能卡 GID 兼容设备。 插使用智能卡的唯一 ID 作为以下：

    1.  GID 兼容设备 ID 作为兼容 id。
    2.  卡片的 ATR 历史个字节作为设备 id。 如果不有任何历史 ATR 字节，插将使用 GID 兼容设备 ID 作为设备 id。

8.  如果插派生而来的智能卡的唯一 ID，它将继续到步骤 12。
9.  如果插无法选择 PIV 辅助工具或 MS GID 辅助工具，它使用卡的 ATR 历史字节数 （如果有） 作为设备 ID 为智能卡的唯一 id。
10. 如果插没有 ATR 历史字节，它没有足够的信息供 Windows 更新。 插失败放弃发现过程\_E\_意外的。
11. 如果插派生而来的智能卡的唯一 ID，它将继续到步骤 12。
12. 插停止发现过程，并使用唯一标识符。

从开始从 Windows 8 中，如果插是找不到卡的驱动程序，与收件箱 NULL 驱动程序配对卡。 特定于卡的其他软件，需要为连接到智能卡读卡器时，对函数卡连接到 PC。

## <a name="span-idwinscarddiscoveryprocessspanspan-idwinscarddiscoveryprocessspanspan-idwinscarddiscoveryprocessspanwinscard-discovery-process"></a><span id="Winscard_Discovery_Process"></span><span id="winscard_discovery_process"></span><span id="WINSCARD_DISCOVERY_PROCESS"></span>Winscard 发现过程


Winscard (Winscard.dll) 发现过程用于将卡与已安装的微型驱动程序关联在系统中。 启动进程时[ **SCardListCards** ](https://msdn.microsoft.com/library/windows/desktop/aa379789)或[ **SCardLocateCards** ](https://msdn.microsoft.com/library/windows/desktop/aa379794)调用。

从 Windows 7 开始，下面介绍的 Winscard 发现过程：

1.  在表示智能卡的计算机中安装的各种子项的 Calais 密钥下的注册表中查找 Winscard。 这些子项位于以下位置：

    HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Cryptography\\Calais\\SmartCards

2.  Winscard 搜索智能卡子项下的每个子项的子项的 ATR 值与从智能卡获取的 ATR 值相匹配。 如果找到匹配项，请转到步骤 6。
3.  Winscard 查找智能卡微型驱动程序子项值与中的 PIV 设备 ATR 缓存 （适用于 PIV 卡） 或 （适用于 Microsoft GID 兼容卡） IDMP ATR 缓存子项的值相匹配。 如果找到匹配项是转到步骤 6。
4.  Winscard 为 MS GID 辅助设备发出 SELECT 命令。 如果此命令成功，请转到步骤 6。
5.  如果步骤 4 失败，Winscard PIV 辅助工具为发出 SELECT 命令。 如果此命令成功，请转到步骤 6。
6.  Winscard 返回的卡片，对应于匹配卡微型驱动程序注册表项的名称。

**请注意**  下表描述 Winscard 发现过程使用的各种注册表项。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">注册表项</th>
<th align="left">将</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft \Cryptography\Calais\SmartCards</td>
<td align="left">Winscard 作为 Calais\SmartCards 键在步骤 1 中使用此密钥。</td>
</tr>
<tr class="even">
<td align="left">HKEY_LOCAL_MACHINE\ SOFTWARE\Microsoft \Cryptography\Calais\PIV Device ATR Cache</td>
<td align="left"><p>如果在步骤 4 中找到匹配，匹配卡完整 ATR 作为二进制值存储在此注册表项。 随机选择项的名称。</p>
<p>此条目已缓存后，它使用在步骤 3 中以提高性能。</p></td>
</tr>
<tr class="odd">
<td align="left">HKEY_LOCAL_MACHINE\ SOFTWARE\Microsoft \Cryptography\Calais\IDMP ATR Cache</td>
<td align="left"><p>如果在步骤 5 中找到匹配，匹配卡完整 ATR 存储在此注册表项下作为二进制值。 随机选择项的名称。</p>
<p>此条目已缓存后，它使用在步骤 3 中以提高性能。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwindowssmartcardclassminidriverdiscoveryprocessspanspan-idwindowssmartcardclassminidriverdiscoveryprocessspanspan-idwindowssmartcardclassminidriverdiscoveryprocessspan-windows-smart-card-class-minidriver-discovery-process"></a><span id="_Windows_Smart_Card_Class_Minidriver_Discovery_Process"></span><span id="_windows_smart_card_class_minidriver_discovery_process"></span><span id="_WINDOWS_SMART_CARD_CLASS_MINIDRIVER_DISCOVERY_PROCESS"></span> Windows 智能卡类微型驱动程序发现过程


Windows 智能卡类微型驱动程序执行以下发现处理何时[ **CardAcquireContext** ](https://msdn.microsoft.com/library/windows/hardware/dn468701)调用。 微型驱动程序执行此发现过程以将相关联的卡标记为 PIV 或 Microsoft GID 兼容：

1.  微型驱动程序的 PIV 辅助设备发出 SELECT 命令。 如果命令成功，将卡标记为 PIV 兼容和发现过程停止。
2.  否则，微型驱动程序为 MS GID 辅助设备发出 SELECT 命令。 如果命令成功或失败来查找辅助设备，微型驱动程序会将卡标记为 MS GID。

**注意**  
-   如果智能卡以前已通过类微型驱动程序 Winscard 发现过程发现的它可能不响应 SELECT 命令 PIV 或 GID 辅助工具。 在此情况下，它必须实现 GID 卡的边缘，并且将自定义帮助的供应商的卡。 此类卡可以扩展 Microsoft 智能卡数据模型与其他数据对象。
-   PIV 和 GID 智能卡供应商可以使用 Windows 智能卡类微型驱动程序，并添加品牌标记，从而仅限 INF 的安装包。 有关使用类微型驱动程序的兼容的卡的详细信息，请参阅中的 INF 示例[智能卡即插](smart-card-plug-and-play.md)。 Plug and play INF 中匹配使用仅历史个字节。

    供应商提供的 INF 文件创建条目下 Calais\\智能卡包含以下信息的注册表子项。

    | 项名称                      | 在任务栏的搜索框中键入   | 值                                     |
    |---------------------------------|--------|-------------------------------------------|
    | 80000001                        | 字符串 | Msclmd.dll                                |
    | ATR                             | Binary | 卡片的 ATR                                |
    | ATRMask                         | Binary | 卡片的 ATR 掩码                           |
    | 加密提供程序                 | 字符串 | Microsoft Base Smart Card Crypto Provider |
    | 智能卡密钥存储提供程序 | 字符串 | Microsoft 智能卡密钥存储提供程序 |

     

 

## <a name="span-idselectionmechanismsspanspan-idselectionmechanismsspanspan-idselectionmechanismsspanselection-mechanisms"></a><span id="Selection_Mechanisms"></span><span id="selection_mechanisms"></span><span id="SELECTION_MECHANISMS"></span>选择机制


### <a name="span-idapplicationsthatcontainmicrosoftidentifiersspanspan-idapplicationsthatcontainmicrosoftidentifiersspanspan-idapplicationsthatcontainmicrosoftidentifiersspanapplications-that-contain-microsoft-identifiers"></a><span id="Applications_that_Contain_Microsoft_identifiers"></span><span id="applications_that_contain_microsoft_identifiers"></span><span id="APPLICATIONS_THAT_CONTAIN_MICROSOFT_IDENTIFIERS"></span>应用程序，包含 Microsoft 标识符

Windows 智能卡框架会尝试通过使用 Microsoft Plug and Play 辅助设备选择一个应用程序。 如果卡不支持指定的辅助设备，则应选择命令后返回错误。 如果 SELECT 命令成功完成，框架将尝试通过发出获取数据命令中标识的卡和相应的智能卡微型驱动程序。

获取数据命令执行而不考虑是否支持 SC 即插即用和播放保持。 这样，应用程序，或者与其他帮助，或者不与任何辅助工具，它们是实现此规范中的卡选择机制。

### <a name="span-idgetdataspanspan-idgetdataspan-get-data"></a><span id="_GET_DATA"></span><span id="_get_data"></span> GET DATA

它将选择插在卡上的 MS 帮助后，智能卡框架与 0x7F68 Windows 专有标记颁发获取数据命令。 如果卡支持的获取数据命令和专有标记，它响应通过返回一个或多个唯一标识符的列表。 必须结构的唯一标识符，如下面的"Windows 智能卡框架卡标识符"部分中定义。

Windows 智能卡框架使用的第一个唯一标识符列表中，找到并安装适当的智能卡微型驱动程序。 可能在将来使用其他标识符。

### <a name="span-idselectpivaidcommandspanspan-idselectpivaidcommandspanspan-idselectpivaidcommandspan-select-piv-aid-command"></a><span id="_SELECT_PIV_AID_Command"></span><span id="_select_piv_aid_command"></span><span id="_SELECT_PIV_AID_COMMAND"></span> 选择 PIV 帮助命令

若要标识 PIV 应用程序，Windows 会发出选择 PIV 帮助命令。 如果此命令成功，PIV 应用程序在卡上存在且当前已选定。 在此情况下，Windows 智能卡框架现在可以将符合 piv 标准的微型驱动程序关联与卡。

### <a name="span-idselectmsgidsaidcommandspanspan-idselectmsgidsaidcommandspanspan-idselectmsgidsaidcommandspan-select-ms-gids-aid-command"></a><span id="_SELECT_MS_GIDS_AID_Command"></span><span id="_select_ms_gids_aid_command"></span><span id="_SELECT_MS_GIDS_AID_COMMAND"></span> 选择 MS GID 帮助命令

若要标识 MS GID 应用程序，使用选择 MS GID 帮助命令。 如果此命令成功，MS GID 应用程序在卡上存在且当前已选定。 Windows 智能卡框架可以现在将兼容 MS GID 的微型驱动程序相关联的卡。

### <a name="span-iduseoftheatrhistoricalbytesspanspan-iduseoftheatrhistoricalbytesspanspan-iduseoftheatrhistoricalbytesspanuse-of-the-atr-historical-bytes"></a><span id="Use_of_the_ATR_Historical_Bytes"></span><span id="use_of_the_atr_historical_bytes"></span><span id="USE_OF_THE_ATR_HISTORICAL_BYTES"></span>使用了 ATR 历史字节

在以下情况下 Windows 智能卡框架将恢复为使用 ATR 历史字节 ATR 确定微型驱动程序加载：

-   智能卡不支持的获取数据命令。
-   智能卡不支持此规范中的辅助设备选择方法。

ATR 历史字节的用途是用来标识插入的卡的旧方法。 框架将使用在其微型驱动程序搜索所有历史字节。

### <a name="span-idwindowssmartcardframeworkcardidentifierspanspan-idwindowssmartcardframeworkcardidentifierspanspan-idwindowssmartcardframeworkcardidentifierspan-windows-smart-card-framework-card-identifier"></a><span id="_Windows_Smart_Card_Framework_Card_Identifier"></span><span id="_windows_smart_card_framework_card_identifier"></span><span id="_WINDOWS_SMART_CARD_FRAMEWORK_CARD_IDENTIFIER"></span> Windows 智能卡框架卡标识符

如果智能卡支持的获取数据命令，Windows 智能卡框架需要卡以返回处于以下的 ASN.1 结构格式化 TLV DER 编码的字节数组。

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

版本成员必须设置为 0 (v1)。

供应商成员必须设置为"MSFT"。

GUID 成员是一个 16 字节 GUID，唯一标识卡/应用程序组合。 此值用于检测并加载适当的智能卡微型驱动程序。

**请注意**  IHV 或 ISV 提供的问题应用程序必须创建其卡/应用程序组合的唯一 GUID。

 

 

 





