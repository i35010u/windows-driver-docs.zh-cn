---
title: 附录4驱动程序签名问题
description: 下面介绍了两个已知的驱动程序签名问题。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83e9b5b80cfde5903c497db067eb5304c6366387
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808171"
---
# <a name="appendix-4-driver-signing-issues"></a>附录 4：驱动程序签名问题


下面介绍了两个已知的驱动程序签名问题。

## <a name="signing-issue-with-previous-os"></a>以前的操作系统的签名问题


Windows 的每个新版本以及随后在发布的 Service Pack 中的根证书、来自 Microsoft 认证的 CA 供应商的根证书、新的或现有的具有新证书的供应商将添加到操作系统映像。 例如，Vista、XP 等。如果正在测试的计算机未连接到 internet，则操作系统可能存在未知的签名问题或未签名的驱动程序问题。 如果正在测试的计算机已连接到 internet，则在安装驱动程序时将自动下载新证书，且不会出现任何问题。 有时，当所测试的计算机未连接到 internet 时，CA 供应商还可以帮助解决问题。

## <a name="code-52-error"></a>代码52错误


有一个已知 bug，适用于 Windows 7 x64 OS，当编录文件)  ( 时，将使用使用 SHA256 的新的 VeriSign 发行签名证书对其进行签名。 如果打开已签名的 cat 文件并查看签名并选择 "详细信息" 选项卡，则会注意到以下内容：

![显示签名的哈希算法的屏幕截图](images/tutorialcertsignaturehashalg.png)

若要解决此问题，你可能会要求 VeriSign 提供替换证书，无需使用 SHA1 哈希算法进行签名。

或者，如果想要保留这两个证书，可以购买另一个 SHA1 证书，并以两个签名对文件进行签名，如下所示。 请注意，只能对 .sys 文件进行双重签名，因为它们是 PE 文件。

```cpp
Signtool sign /fd sha256 /ac C:\MyCrossCert\Crosscert.cer /s my /n “MyCompany Inc. “ /ph /as /sha1 XX...XX C:\DriverDir\toaster.SYS
```

其中 XX .。。XX 是用于辅助签名的证书哈希。 将/tr 添加到时间戳签名。

**注意**  请查看 Microsoft 安全公告 ([2880823](/security-updates/SecurityAdvisories/2016/2880823)) "弃用适用于 Microsoft 根证书计划的 Sha-1 哈希算法"，其中描述了在年1月 1 2016 日之后，Microsoft 将不再允许根证书颁发机构使用 sha-1 哈希算法颁发 x.509 证书的策略更改。

 

从2016年1月1日开始，Microsoft 不推荐使用 SHA1 证书。 所有 CA 供应商必须用 SHA256 哈希算法颁发签名证书。

2016年1月1日之后，Windows 将停止接受不带时间戳的 SHA1 代码签名证书。

 

