---
Description: 本主题介绍特定于设备的注册表项。
title: USB 设备注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b8308e45f36a8261a2787ebbfed7160745f2e3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384524"
---
# <a name="usb-device-registry-entries"></a>USB 设备注册表项


本主题介绍特定于设备的注册表项。

## <a name="find-device-information-after-it-enumerates-on-windows"></a>它在 Windows 上枚举后找到设备信息


**查看有关设备的 GUID、 硬件 Id 和设备类信息的设备接口**

1.  查找此注册表项并记下**DeviceInstance**值：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses\\**

    ![usb 硬件 id](images/deviceinstance.png)

2.  查找设备实例注册表项和获取设备接口的 GUID:

    **HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\枚举\\USB\\&lt;硬件 id&gt; \\ &lt;实例 id&gt;\\设备参数**

    ![usb 设备接口 guid](images/device-interface-guid2.png)

3.  下设备实例键，请注意设备类、 子类别中，和协议代码：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB**

    ![usb 设备类子类协议代码](images/deviceclass.png)

## <a name="registry-settings-for-configuring-usb-driver-stack-behavior"></a>用于配置 USB 驱动程序堆栈行为的注册表设置


本主题中所述的注册表项位于此项下：

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         Control
            usbflags
               <VVVVPPPPRRRR>
                  <Device-specific registry entry>
```

在中***vvvvpppprrrrr***键，

-   *vvvv*是一个 4 位十六进制数字，标识供应商
-   *pppp*是一个 4 位十六进制数字，标识的产品
-   *rrrr*是 4 位十六进制数字包含设备的修订号。

从获取供应商 ID、 产品 ID 和修订号的值[USB 设备描述符](usb-device-descriptors.md)。
下表描述了可能的注册表条目***vvvvpppprrrrr***密钥。 USB 驱动程序堆栈将这些项视为只读的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表项</th>
<th>描述</th>
<th>可能值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>osvc</strong></p>
<p>REG_BINARY</p>
<p>在 Windows XP 和更高版本上受支持。</p></td>
<td><p>指示操作系统是否查询的设备<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft-Defined USB Descriptors](microsoft-defined-usb-descriptors.md)">Microsoft-Defined USB 描述符</a>。 如果以前尝试 OS 描述符查询成功，此值将包含 OS 字符串描述符中的供应商代码。</p></td>
<td><ul>
<li><p>0x0000:设备未提供对 Microsoft 操作系统字符串描述符请求的有效响应。</p></li>
<li><p>0x01xx:设备提供对 Microsoft 操作系统字符串描述符请求，其中，xx 是有效的响应<strong>bVendorCode</strong>包含在响应中。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>IgnoreHWSerNum</strong></p>
<p>REG_BINARY</p>
<p>在 Windows Vista 和更高版本上受支持。</p></td>
<td><p>指示是否 USB 驱动程序堆栈必须忽略设备序列号。</p></td>
<td><ul>
<li><p>0x0000:设置处于禁用状态。</p></li>
<li><p>0x0001:强制 USB 驱动程序堆栈，若要忽略的设备的序列号。 因此，设备实例将关联到设备附加到的端口。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>ResetOnResume</strong></p>
<p>REG_BINARY</p>
<p>在 Windows Vista 和更高版本上受支持。</p></td>
<td><p>指示是否 USB 驱动程序堆栈必须重置设备时从睡眠周期恢复该端口。</p></td>
<td><ul>
<li><p>0x0000:设置处于禁用状态。</p></li>
<li><p>0x0001:强制重置端口上的设备的 USB 驱动程序堆栈恢复。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



