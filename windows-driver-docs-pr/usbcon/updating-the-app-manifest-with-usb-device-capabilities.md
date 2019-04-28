---
Description: 本主题介绍所需的使用 Windows.Devices.Usb 命名空间的 Windows 应用的设备功能。
title: 如何将 USB 设备功能添加到应用部件清单
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 013695e2f0990172d3a79304f96dda4a9f0db553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355095"
---
# <a name="how-to-add-usb-device-capabilities-to-the-app-manifest"></a>如何将 USB 设备功能添加到应用部件清单


**摘要**

-   使用 USB 设备功能，必须更新 Package.appxmanifest。
-   设备类必须是一个受支持的类。

本主题介绍使用 Windows 应用所需的设备功能[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)命名空间。

## <a name="usb-device-capability-usage"></a>USB 设备功能使用情况


USB 应用必须包括在某些设备功能及其[应用程序包清单](https://msdn.microsoft.com/library/windows/apps/br211474)指定设备有关的关键信息。 以下是所需的元素层次结构顺序：

[**&lt;DeviceCapability&gt;**](https://msdn.microsoft.com/library/windows/apps/br211430):**名称**属性必须为"usb"。

**&lt;设备&gt;**:**Id**属性必须指定供应商/产品 Id，也可以是"any"，以允许访问的函数类型匹配的任何设备。

**&lt;函数&gt;**:**类型**特性可以指定设备类代码、 名称或设备接口的 GUID。

**请注意**  不能修改 Microsoft Visual Studio 2013 中的 USB 设备功能。 您必须右键单击 Package.appxmanifest 文件中的**解决方案资源管理器**，然后选择**打开方式...**，然后**XML （文本） 编辑器**。 在纯 XML 中打开该文件。

 

```XML
<DeviceCapability Name="usb">
    <Device Id="vidpid:xxxx xxxx">
      <Function Type="classId:xx xx xx"/>
      <Function Type="name:xxxxx"/>
      <Function Type="winUsbId:xxxxx"/>
    </Device>
</DeviceCapability>
```

## <a name="supported-usb-device-classes"></a>受支持的 USB 设备类


-   名称和受支持的设备类的代码值如下所示：

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **请注意**  属于 DeviceFirmwareUpdate 类的设备只能访问由该电脑的显式声明由 OEM 的特权应用。

     

-   由于这些是未知的接口，则必须应用，以指定这些类代码的供应商/产品 id。

    -   CDC (0x02)
    -   CDC 数据 (0x0A)
    -   杂项 (0xEF)
    -   特定于应用程序 (0xFE)
    -   特定于供应商 (0xFF)
-   不支持这些 USB 设备类：

    -   无效的类 (0x00)
    -   音频类 (0x01)
    -   HID 的 class(0x03)
    -   图像类 (0x06:sp)
    -   打印机类 (0x07)
    -   大容量存储类 (0x08)
    -   智能卡类 (0x0B)
    -   音频/视频类 (0x10)
    -   无线 (0xE0) 的控制器 （例如，无线 USB 主机/集线器）

## <a name="usb-device-capability-example"></a>USB 设备功能的示例


下面是用于定义 USB 设备功能的一些示例：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>示例</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="any"&gt;
    &lt;Function Type="classId:ef 01 01"/&gt;
    &lt;Function Type="name:stillImage"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用程序访问在任何设备上的任何 ActiveSync 或 StillImage 接口。 应用程序不需要指定供应商/产品标识符，因为这些已知类类型。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="name:vendorSpecific"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用程序访问 OSR USB Fx2 设备上的特定于供应商的接口。</p></td>
</tr>
<tr class="odd">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="classId:ff * <em>"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用程序访问其他版本的 OSR USB Fx2 设备上的特定于供应商的接口。 请注意 classId 格式:"ff * *"。 类代码是"ff"后跟一个通配符 (</em>) 以包含任何代码，子类和协议。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id=" vidpid:1234 5678"&gt;
    &lt;Function Type="winUsbId:"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用程序访问 MS OS 描述符中或在设备 INF 中定义的 GUID 的设备接口的设备。</p>
<p>在这种情况下，设备 Id 值必须等于"any"。</p></td>
</tr>
</tbody>
</table>

 

**应用清单 CustomUsbDeviceAccess 示例包**

```xml
  <Capabilities>
      <!--When the device's classId is FF * *, there is a predefined name for the class. You can use the name instead of the class id. 
          There are also other predefined names that correspond to a classId.-->
      <m2:DeviceCapability Name="usb">
          <!--OSRFX2 Device-->
          <m2:Device Id="vidpid:0547 1002">
              <m2:Function Type="classId:ff * *"/>
              <!--<m2:Function Type="name:vendorSpecific"/>-->
          </m2:Device>
          <!--SuperMutt Device-->
          <m2:Device Id="vidpid:045E 0611">
              <!--<m2:Function Type="classId:ff * *"/>-->
              <m2:Function Type="name:vendorSpecific"/>
          </m2b:Device>
      </m2:DeviceCapability>
  </Capabilities>
```

## <a name="related-topics"></a>相关主题
[USB 设备的 UWP 应用](writing-usb-device-companion-apps-for-microsoft-store.md)  



