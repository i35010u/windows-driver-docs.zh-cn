---
title: AVStream 子设备
description: AVStream 子设备
keywords:
- 子设备 WDK AVStream
- AVStream 子设备 WDK
- 总线枚举 WDK AVStream
- 硬件 Id WDK AVStream
- 标识符 WDK AVStream
- 兼容 Id WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb86b70a7ce28e946f51857274a54aeaad3afa3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815843"
---
# <a name="avstream-child-devices"></a>AVStream 子设备





本部分仅适用于在该平台上安装了 DirectX 9.0 或更高版本的 Microsoft Windows Server 2003 及更早版本的操作系统。

AVStream 可充当设备的总线枚举器，为 **枚举** 分支中的每个密钥创建一个子设备。 为此，请在注册表中的设备密钥下放置一个 **枚举** 分支。

具体而言，在驱动程序的 INF 文件的 **AddReg** 节中，供应商为 Enum 下的每个条目提供类型为 REG SZ 的值 *pnpid* \_ 。 **Enum** AVStream 使用此字符串值为每个单独的子设备构造即插即用 (PnP) 硬件 ID。

在低于 DirectX 9.0 的版本中，AVStream 创建 "AVStream \\ *&lt; pnpid &gt;*" 形式的子设备硬件 ID (其中， &lt; pnpid &gt; 是特定设备) 的 *pnpid* 值。

例如，供应商在 INF 文件的 " **AddReg** " 部分指定以下内容：

```INF
[MyTVDevice.AddReg]
HKR,"ENUM\CrossbarDevice",pnpid,,"MyCrossbar"
HKR,"ENUM\TunerDevice",pnpid,,"MyTuner"
```

相应地，AVStream 将创建具有以下设备 Id 的两个子设备：

AVStream \\ MyCrossbar

AVStream \\ MyTuner

若要解决指定相同 *pnpid* 值的两个不同子设备可能存在的歧义，DirectX 9.0 和更高版本将更改为每个子设备报告的 id。 对于父设备报告的每个硬件 ID，AVStream 将按以下格式为子设备创建 ID：

AVStream \\ *&lt; pnpid &gt;* \# *&lt; 修改的父硬件 &gt; ID*

修改后的父硬件 ID 是具有每个反斜杠的父硬件 ID (**\\**) 字符由数字符号 (**\#**) 替换。

如果生成的字符串太长，AVStream 将以最大 \_ 设备 \_ id \_ 长度字符（包括 **NULL** 终止符）终止 ID 字符串。 在 Windows Server 2003 中，此限制设置为 *cfgmgr32* 中的200个字符。

例如，父设备报告以下硬件 Id：

PCI \\ 即使 \_ XXXX&DEV \_ YYYY&子系统 \_ ZZZZZZZZ&REV \_ VV

PCI \\ 即使 \_ XXXX&DEV \_ YYYY&子系统 \_ ZZZZZZZZ

对于 *pnpid* 密钥为 **MyCrossbar** 的设备，AVStream 会创建以下子设备硬件 id：

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&DEV \_ YYYY&子系统 \_ ZZZZZZZZ&REV \_ VV

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&DEV \_ YYYY&子系统 \_ ZZZZZZZZ

AVStream 对父设备报告的兼容 Id 使用相同的过程。 AVStream 为以下格式的子设备创建一个兼容的 ID：

AVStream \\ *&lt; pnpid &gt;* \# *&lt; 修改了父兼容 &gt; ID*

兼容 Id 的名称修改和长度规则与硬件 Id 的修改和长度规则完全相同。

例如，如果前面介绍的父设备报告以下兼容 Id：

PCI \\ 即使 \_ XXXX&DEV \_ YYYY&REV \_ VV

PCI \\ 即使 \_ XXXX&DEV \_ YYYY

PCI \\ 即使 \_ XXXX&CC \_ ZZZZZZ

PCI \\ 即使 \_ XXXX&CC \_ ZZZZ

PCI \\ 即使 \_ XXXX

PCI \\ CC \_ ZZZZZZ

PCI \\ CC \_ ZZZZ

**MyCrossbar** 子设备将通过 AVStream 以下兼容 id 进行报告：

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&DEV \_ YYYY&REV \_ VV

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&DEV \_ YYYY

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&CC \_ ZZZZZZ

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX&CC \_ ZZZZ

AVStream \\ MyCrossbar \# PCI \# 即使 \_ XXXX

AVStream \\ MyCrossbar \# PCI \# CC \_ ZZZZZZ

AVStream \\ MyCrossbar \# PCI \# CC \_ ZZZZ

AVStream \\ MyCrossbar

**注意**  在 DirectX 9.0 和更高版本中，旧的硬件 id AVStream \\ *&lt; &gt; pnpid* 仍报告为最低排名兼容 ID。 因此，旧驱动程序在这些平台上仍可继续工作。
但是，在 DirectX 9.0 版本中，Microsoft 建议供应商编写新的或经过修改的、利用 AVStream 类总线枚举器的驱动程序使用新的硬件 ID 格式。 驱动程序可以通过将旧 ID 包含在 INF 文件中的兼容 Id 列表中，来支持运行早期版本的 AVStream 的平台。

 

 

 




