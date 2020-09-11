---
description: 本主题介绍使用 Windows Usb 命名空间的 Windows 应用程序所需的设备功能。
title: 如何将 USB 设备功能添加到应用部件清单
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: d4ac43092a985723e57e0f853efb3040be9d65b6
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010439"
---
# <a name="how-to-add-usb-device-capabilities-to-the-app-manifest"></a>如何将 USB 设备功能添加到应用部件清单


**摘要**

-   必须用 USB 设备功能更新 appxmanifest.xml。
-   设备类必须是受支持的类之一。

本主题介绍使用 [**Windows Usb**](/uwp/api/Windows.Devices.Usb) 命名空间的 windows 应用程序所需的设备功能。

## <a name="usb-device-capability-usage"></a>USB 设备功能使用情况


USB 应用必须在其 [应用程序包清单](/uwp/schemas/appxpackage/appx-package-manifest) 中包含某些设备功能，以指定有关设备的关键信息。 下面是按层次顺序排列的必需元素：

[** &lt; DeviceCapability &gt; **](/uwp/schemas/appxpackage/appxmanifestschema/element-devicecapability)： **Name**属性必须是 "usb"。

** &lt; 设备 &gt; **： **Id**属性必须指定供应商/产品 Id 或 "任何"，以允许访问与该函数类型匹配的任何设备。

** &lt; 函数 &gt; **： **Type**特性可以指定设备类代码、名称或设备接口 GUID。

**注意**   无法在 Microsoft Visual Studio 2013 中修改 USB 设备功能。 必须右键单击 **解决方案资源管理器** 中的 appxmanifest.xml 文件，然后选择 " **打开方式 ...**"，然后选择 " **XML (文本) 编辑器**"。 文件以纯 XML 格式打开。

 

```XML
<DeviceCapability Name="usb">
    <Device Id="vidpid:xxxx xxxx">
      <Function Type="classId:xx xx xx"/>
      <Function Type="name:xxxxx"/>
      <Function Type="winUsbId:xxxxx"/>
    </Device>
</DeviceCapability>
```

## <a name="supported-usb-device-classes"></a>支持的 USB 设备类


-   支持的设备类的名称和代码值如下所示：

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **注意**   属于 DeviceFirmwareUpdate 类的设备只能由 OEM 为该 PC 显式声明的特权应用程序访问。

     

-   由于这些是未知接口，因此应用需要为这些类代码指定供应商/产品 id。

    -   CDC (0x02) 
    -   CDC-data (0x0A) 
    -   0xEF) 的其他 (
    -   特定于应用程序 (0xFE) 
    -   特定于供应商 (0xFF) 
-   不支持这些 USB 设备类：

    -    (0x00 的类无效) 
    -   音频类 (0x01) 
    -   HID 类 (0x03) 
    -   Image 类 (0x06) 
    -   Printer 类 (0x07) 
    -   大容量存储类 (0x08) 
    -   智能卡类 (0x0B) 
    -   音频/视频类 (0x10) 
    -   无线控制器 (如无线 USB 主机/集线器)  (0xE0) 

## <a name="usb-device-capability-example"></a>USB 设备功能示例


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
<td><p>允许应用访问任何设备上的任何 ActiveSync 或 StillImage 接口。 应用无需指定供应商/产品标识符，因为这些是已知类类型。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="name:vendorSpecific"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用访问 OSR USB Fx2 设备上的特定于供应商的接口。</p></td>
</tr>
<tr class="odd">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id="vidpid:045e 930a"&gt;
    &lt;Function Type="classId:ff * <em>"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用程序在不同版本的 OSR USB Fx2 设备上访问供应商特定的接口。 请注意 classId 格式： "ff * *"。 类代码是 "ff" 后跟通配符 (</em>) 以包括任何子类和协议代码。</p></td>
</tr>
<tr class="even">
<td><pre class="syntax" space="preserve"><code class="language-xml">&lt;DeviceCapability Name="usb"&gt;
  &lt;Device Id=" vidpid:1234 5678"&gt;
    &lt;Function Type="winUsbId:"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"/&gt;
  &lt;/Device&gt;
&lt;/DeviceCapability&gt;</code></pre></td>
<td><p>允许应用使用在 MS OS 描述符或设备 INF 中定义的设备接口 GUID 来访问设备。</p>
<p>在这种情况下，设备 Id 值不得等于 "任何"。</p></td>
</tr>
</tbody>
</table>

 

**CustomUsbDeviceAccess 示例的应用程序清单包**

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