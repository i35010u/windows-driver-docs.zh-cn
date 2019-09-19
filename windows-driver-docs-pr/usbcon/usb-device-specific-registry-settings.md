---
Description: 本主题介绍特定于设备的注册表项。
title: USB 设备注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40c32d3c6b425b11ca9ffbc027611798cb51f071
ms.sourcegitcommit: 4943143e8395db70beda5a98ad734fe1bb7068dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2019
ms.locfileid: "71080187"
---
# <a name="usb-device-registry-entries"></a>USB 设备注册表项


本主题介绍特定于设备的注册表项。

## <a name="find-device-information-after-it-enumerates-on-windows"></a>在 Windows 上枚举后查找设备信息


**查看设备接口 GUID、硬件 Id 和设备类有关设备的信息**

1.  找到此注册表项并记下**DeviceInstance**值：

    **HKEY\_本地\_计算机系统\\CurrentControlSet\\控制DeviceClasses\\\\\\**

    ![usb 硬件 id](images/deviceinstance.png)

2.  查找设备实例注册表项并获取设备接口 GUID：

    **HKEY\_本地\_计算机系统\\CurrentControlSet\\枚举USB\\硬件 id&gt; \\\\\\&lt;&lt;实例 id&gt;设备参数\\**

    ![usb 设备接口 guid](images/device-interface-guid2.png)

3.  在设备实例密钥下，记下设备类、子类和协议代码：

    **HKEY\_本地\_计算机系统\\CurrentControlSet\\枚举USB\\\\**

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

在***vvvvpppprrrrr***项中，

-   *vvvv*是用于标识供应商的四位十六进制数
-   *pppp*是用于标识产品的四位十六进制数
-   *rrrr*是一个4位十六进制数字，其中包含设备的修订号。

供应商 ID、产品 ID 和修订号值是从[USB 设备描述符](usb-device-descriptors.md)获取的。
下表描述了***vvvvpppprrrrr***项的可能的注册表项。 USB 驱动程序堆栈会将这些项视为只读值。

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
<p>在 Windows XP 及更高版本上受支持。</p></td>
<td><p>指示操作系统是否在设备上查询了<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft-Defined USB Descriptors](microsoft-defined-usb-descriptors.md)">Microsoft 定义的 USB 描述符</a>。 如果以前尝试的操作系统描述符查询成功，则该值包含 OS 字符串描述符中的供应商代码。</p></td>
<td><ul>
<li><p>0x0000设备未提供对 Microsoft OS 字符串描述符请求的有效响应。</p></li>
<li><p>0x01xx:设备提供了对 Microsoft OS 字符串描述符请求的有效响应，其中 xx 是响应中包含的<strong>bVendorCode</strong> 。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>IgnoreHWSerNum</strong></p>
<p>REG_BINARY</p>
<p>在 Windows Vista 和更高版本上受支持。</p></td>
<td><p>指示 USB 驱动程序堆栈是否必须忽略设备的序列号。</p></td>
<td><ul>
<li><p>0x00禁用该设置。</p></li>
<li><p>0x01强制 USB 驱动程序堆栈忽略设备的序列号。 因此，设备实例与设备连接到的端口相关联。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>ResetOnResume</strong></p>
<p>REG_BINARY</p>
<p>在 Windows Vista 和更高版本上受支持。</p></td>
<td><p>指示当端口从睡眠周期恢复时，USB 驱动程序堆栈是否必须重置设备。</p></td>
<td><ul>
<li><p>0x0000禁用该设置。</p></li>
<li><p>0x0001强制 USB 驱动程序堆栈在恢复端口时重置设备。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



