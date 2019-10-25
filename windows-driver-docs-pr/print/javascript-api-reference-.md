---
title: JavaScript API 参考
description: 结合使用 JavaScript API 和双向 XML 文件，为到打印设备的 USB 连接提供支持。
ms.assetid: 604DF74E-AEF1-43DC-81B2-566A94B1CE8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4c46ecc767bdb45718e39e2e25bf818b1bc107
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828931"
---
# <a name="javascript-api-reference"></a>JavaScript API 参考


制造商可以使用此处提供的 JavaScript API，并将其与双向 XML 文件结合使用，以便通过 USB 连接到打印设备来支持双向。

有关与打印设备进行 USB 双向通信的详细信息，请参阅[Usb 双向扩展](usb-bidi-extender.md)器。

## <a name="bidi-over-usb"></a>USB 上的双向


## <a name="getschemas-method"></a>getSchemas 方法


此方法处理双向获取查询，如 \\YellowInk： Level。 JavaScript 代码可以使用 USB 总线在打印机上进行查询，并在恢复时读取响应。

语法

```javascript
function getSchemas(scriptContext, printerStream, schemaRequests, printerBidiSchemaResponses);
```

参数

*scriptContext*

\[在\] 提供对相关属性包的访问的[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)对象。
*printerStream*

\] 中的 \[允许对 USB 总线进行读写访问的[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)对象。
*schemaRequests*

\[包含所有请求的双向查询字符串\] 数组对象。
*printerBidiSchemaResponses*

\[\] 对象，该脚本使用该对象来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 脚本已成功完成。                                                                                                                                                      |
| 1            | 连接的设备尚未准备好提供某些请求的信息。 指示打印系统应使用在处理过程中添加的任何 Requery 键再次调用函数。 |



## <a name="setschema-method"></a>setSchema 方法


此方法处理双向集运算。 此脚本可以确定传入的双向架构值，以设置设备中的数据，或者在设备上执行某些操作，如清洁墨打印头。

如果设备尚未准备好处理指定的数据，则该方法返回的值为1，指示应在等待期后重试该调用。

参数

*scriptContext*

\[在\] 提供对相关属性包的访问的[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)对象。
*printerStream*

\] 中的 \[允许对 USB 总线进行读写访问的[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)对象。
*printerBidiSchemaElement*

中 \[\] 一个[IPrinterBidiSchemaElement](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaelement-interface)对象，该对象包含与要设置的双向架构值相关联的所有数据。
返回值

| 返回值 | 描述                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 脚本已成功完成。                                                                                                                                                   |
| 1            | 连接的设备尚未准备好提供某些请求的信息。 指示打印系统应使用提供的 printerBidiSchemaElement 再次调用函数。 |



## <a name="getstatus-method"></a>getStatus 方法


此方法用于在设备打印时从打印机获取未经请求的状态。 仅在打印期间调用此函数。 设备应在读取通道上提供数据，此脚本可以将其解释为双向架构值。 由于打印数据阻止了写入到设备的通道，因此此处仅支持未经请求的状态。

在打印过程中将重复调用此方法。 设备应只返回数据（如果可用），并且该脚本可以理解数据。 如果设备不支持未经请求的状态，或者无需再次调用此函数，则脚本应返回值2，这将告知 USBMon 中的**getStatus**执行线程成功退出。

参数

*scriptContext*

\[在\] 提供对相关属性包的访问的**IPrinterScriptContext**对象。
*printerStream*

\] 中的 \[允许对 USB 总线进行读取访问的[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)对象。
*printerBidiSchemaResponses*

\[\] 对象，该脚本使用该对象来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------|
| 0            | 脚本已成功完成。                                                                      |
| 2            | 附加设备不再支持未经请求的状态，因此不应再次调用此函数。 |



## <a name="startprintjob-method"></a>startPrintJob 方法


USBMon 在 StartDocPort 期间调用此方法。 通过调用**startPrintJob** ，驱动程序可以修改打印流，或实现在打印设备打印作业时使用的基于主机的请求/响应协议。 将作业上下文对象传递到函数，以允许制造商的 JavaScript 代码管理作业属性并访问永久性数据流。 打印数据作为 JavaScript 数组传入，以便 JavaScript 代码进行处理。 **startPrintJob**还通过以下方式提供对打印机设备的访问权限：

-   通过打印流

-   通过可返回 USBMon 到进程的双向架构响应的对象

语法

```javascript
function startPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

参数

*jobScriptContext*

\[中\] 一个[**IPrinterScriptUsbJobContext**](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterscriptusbjobcontext)对象，该对象为制造商提供对作业属性包和永久性数据流的 JavaScript 代码访问权限。
*printerStream*

\[\] **IPrinterScriptableSequentialStream**对象中，制造商的 JavaScript 代码可以使用该对象在打印设备上读取和写入数据。
*printerBidiSchemaResponses*

\[\] 制造商的 JavaScript 代码可用于返回任何双向架构值更改/更新的[**IPrinterBidiSchemaResponses**](https://docs.microsoft.com/windows-hardware/drivers/print/iprinterbidischemaresponses)对象。

| 返回值 | 描述                                                                             |
|--------------|-----------------------------------------------------------------------------------------|
| 0            | 辉煌.                                                                                |
| 1            | 失败–清除作业上下文对象并将错误代码返回到打印后台处理程序。 |



## <a name="writeprintdata-method"></a>writePrintData 方法


USBMon 在 writePort 期间调用此方法。 通过调用**writePrintData** ，驱动程序可以修改打印流，或实现在打印设备打印作业时使用的基于主机的请求/响应协议。 作业上下文对象将被传递到方法中，以允许制造商的 JavaScript 代码管理作业属性并访问永久性数据流。 打印数据作为 JavaScript 数组传入，以便 JavaScript 代码进行处理。 **writePrintData**还通过以下方式提供对打印机设备的访问权限：

-   通过打印流

-   通过可返回 USBMon 到进程的双向架构响应的对象

```javascript
function writePrintData(jobScriptContext, writePrintDataProgress, printData, printerStream, printerBidiSchemaResponses);
```

参数

*jobScriptContext*

\[中\] 一个**IPrinterScriptUsbJobContext**对象，该对象为制造商提供对作业属性包和永久性数据流的 JavaScript 代码访问权限。
*writePrintDataProgress*

\[\] 制造商的 JavaScript 代码可用于在打印设备上读取和写入数据的**IPrinterScriptableSequentialStream**对象。
*printData*

\[中\] **IDispatch**对象，这是当前打印数据的 JavaScript 数组。 *PrintData*参数允许 JavaScript 代码在将数据缓存到*jobScriptContext*中的数据流之一之前操作数据，或通过*printerStream*将数据发送到打印机。
*printerStream*

\[\] 制造商的 JavaScript 代码可用于在打印设备上读取和写入数据的**IPrinterScriptableSequentialStream**对象。
*printerBidiSchemaResponses*

\[\] 制造商的 JavaScript 代码可用于返回任何双向架构值更改或更新的**IPrinterBidiSchemaResponses**对象。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0</td>
<td>辉煌. 从打印数据流（<em>printData</em>）处理的字节数通过<em>writePrintDataProgress</em>返回。</td>
</tr>
<tr class="even">
<td>1</td>
<td>失败–将错误代码返回到打印后台处理程序。</td>
</tr>
<tr class="odd">
<td>2</td>
<td><p>重试-在<em>printerBidiSchemaResponses</em>中处理所有双向架构更新（包括双向事件），然后再次调用 JavaScript 函数，以允许制造商的代码继续处理数据。</p>
<p>从打印数据流（<em>printData</em>）处理的字节数通过<em>writePrintDataProgress</em>返回。</p></td>
</tr>
<tr class="even">
<td>3</td>
<td><p>DeviceBusy –设备通信通道目前不接受数据。 这并不表示出现故障。 USBMon 应通知后台处理程序设备处于繁忙状态，然后再次调用该函数。</p>
<p>从打印数据流（<em>printData</em>）处理的字节数通过<em>writePrintDataProgress</em>返回。</p></td>
</tr>
<tr class="odd">
<td>4</td>
<td>AbortTheJob-设备无法继续处理作业，或用户已使用打印设备的前面板取消了作业。 当 USBMon 收到用于中止打印作业的消息时，它会将信息传递给打印后台处理程序，以在返回前中止作业。</td>
</tr>
</tbody>
</table>



## <a name="endprintjob-method"></a>endPrintJob 方法


USBMon 在 endDocPort 期间调用此方法。 通过调用**endPrintJob** ，驱动程序可以修改打印流，或实现在打印设备打印作业时使用的基于主机的请求/响应协议。 作业上下文对象将传递到方法，以允许制造商的 JavaScript 代码执行以下操作：

-   处理完保存的所有打印数据

-   通过打印流访问打印机设备

-   访问一个对象，该对象可传递 USBMon 的双向架构响应来处理

```javascript
function endPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

参数

*jobScriptContext*

\[中\] 一个 IPrinterScriptUsbJobContext 对象，该对象为制造商提供对作业属性包和永久性数据流的 JavaScript 代码访问权限。
*printerStream*

\[\] 制造商的 JavaScript 代码可用于在打印设备上读取和写入数据的 IPrinterScriptableSequentialStream 对象。
*printerBidiSchemaResponses*

\[\] 制造商的 JavaScript 代码可用于返回任何双向架构值更改或更新的 IPrinterBidiSchemaResponses 对象。

| 返回值 | 描述                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 成功–清除作业上下文对象并将成功返回到打印后台处理程序。                                                                                                                                         |
| 1            | 失败–清除作业上下文对象并将错误代码返回到打印后台处理程序。                                                                                                                                   |
| 2            | 重试-在*printerBidiSchemaResponses*中处理所有双向架构更新（包括双向事件），然后再次调用 JavaScript 函数，以允许制造商的 javascript 代码继续处理数据。 |



## <a name="bidi-over-secondary-usb"></a>辅助 USB 上的双向


如果设备支持辅助 USB 接口，则除了**requestStatus**方法之外，设备还可以使用前面几节中所述的**getSchemas**和**setSchema**方法。

## <a name="requeststatus-method"></a>requestStatus 方法


如果在 v4 驱动程序的清单文件中指定了**BidiUSBStatusInterface**指令，则会调用此方法，而不是**getStatus**。 **requestStatus**用于在设备打印时从打印设备获取状态。

下图提供了 USB 双向扩展体系结构的概述，其中显示了已指定**BidiUSBStatusInterface**指令并因此通信通过备用 USB 接口路由的情况。

![带有 requeststatus 方法的 usb 双向扩展器体系结构](images/usbbidiext-arch2.png)

在打印过程中将重复调用此方法。 设备应只返回数据（如果可用），并且该脚本可以理解数据。 如果设备不支持请求的状态，或者无需再次调用此方法，则脚本应返回值2，这将告知 USBMon 中的**getStatus**执行线程成功退出。

参数

*scriptContext*

\[在\] 提供对相关属性包的访问的**IPrinterScriptContext**对象。
*printerStream*

\] 中的 \[允许对 USB 总线进行读写访问的**IPrinterScriptableSequentialStream**对象。
*printerBidiSchemaResponses*

\[\] 对象，该脚本使用该对象来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------|
| 0            | 脚本已成功完成。                                                                    |
| 2            | 附加设备不再支持请求的状态，因此不应再次调用此函数。 |



## <a name="related-topics"></a>相关主题
[**IPrinterScriptContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptcontext)  
[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)  
[USB 双向扩展器](usb-bidi-extender.md)  



