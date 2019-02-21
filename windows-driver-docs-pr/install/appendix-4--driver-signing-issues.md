---
title: 附录 4 驱动程序签名问题
description: 两个已知的驱动程序签名问题如下所述。
ms.assetid: EC244022-A02B-4AAD-93EE-B9AE3E72A674
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1592fab6e387c7d4c01c005e62dcdaad77403b96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520794"
---
# <a name="appendix-4-driver-signing-issues"></a>附录 4:驱动程序签名问题


两个已知的驱动程序签名问题如下所述。

## <a name="signing-issue-with-previous-os"></a>签名与以前的操作系统的问题


每个新版本的 Windows 并随后在已发布的服务包中，来自 Microsoft 的根证书认证的 CA 供应商、 新的或现有的供应商，使用新证书添加到 OS 映像。 例如，Vista、 XP、 支持等。操作系统可能具有未知问题或驱动程序的签名不签名问题，如果待测试的计算机未连接到 internet。 如果待测试的计算机连接到 internet，然后将新证书会自动下载时安装的驱动程序并将不会有任何问题。 有时 CA 供应商就还能够帮助解决问题的测试计算机未连接到 internet 时解决问题。

## <a name="code-52-error"></a>代码 52 错误


Windows 7 x64 OS，目录文件 (.cat) 时使用新 VeriSign 已发布的签名证书的使用 SHA256 进行签名的算法是一个已知的 bug。 如果您打开的有符号的 cat 文件和视图的签名并选择详细信息选项卡会发现以下：

![显示签名的哈希算法的屏幕截图](images/tutorialcertsignaturehashalg.png)

若要解决此问题，可能会要求 VeriSign 提供免费使用 SHA1 哈希算法签名的替换证书。

或者，可以购买其他 SHA1 证书，并带有两个签名文件，如下所示是否想要保留这两个证书进行签名。 请注意，只有.sys 文件可以是双签名，因为它们为 PE 文件。

```cpp
Signtool sign /fd sha256 /ac C:\MyCrossCert\Crosscert.cer /s my /n “MyCompany Inc. “ /ph /as /sha1 XX...XX C:\DriverDir\toaster.SYS
```

其中 XX...XX 是用于辅助签名证书的哈希。 向/t 时间戳签名。

**请注意**  请查看 Microsoft 安全公告 ([2880823](https://technet.microsoft.com/library/security/2880823))"不推荐使用的 sha-1 哈希算法为 Microsoft 根证书计划"其中描述了策略更改，其中 Microsoft 将会不再允许根证书颁发机构颁发 X.509 证书的 sha-1 哈希算法用于 SSL 和代码签名 2016 年 1 月 1 日之后的用途。

 

将由 Microsoft 从 2016 年 1 月 1 日开始弃用 SHA1 证书的使用。 所有 CA 供应商都必须颁发签名证书使用 SHA256 哈希算法。

Windows 将停止接受 SHA1 代码签名后 1 2016 年 1 月没有时间戳的证书。

 

 





