---
title: JavaScript API 参考
description: 使用 JavaScript API 结合使用 Bidi XML 文件通过 USB 连接到打印设备提供支持。
ms.assetid: 604DF74E-AEF1-43DC-81B2-566A94B1CE8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80f04f419ca1fbf2c6e8f1938264b6c5a6fa4cd0
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349080"
---
# <a name="javascript-api-reference"></a>JavaScript API 参考


制造商也可以使用 JavaScript API 在此处，以使用 Bidi XML 文件以提供对 Bidi 通过 USB 连接到打印设备的支持的组合。

有关与打印设备的 USB Bidi 通信的详细信息，请参阅[USB Bidi 扩展器](usb-bidi-extender.md)。

## <a name="bidi-over-usb"></a>通过 USB Bidi


## <a name="getschemas-method"></a>getSchemas 方法


此方法可处理 Bidi 获取查询如\\Printer.Consumables.YellowInk:Level。 JavaScript 代码就能够使用 USB 总线的打印机进行的查询和读取他们返回的响应。

语法

```javascript
function getSchemas(scriptContext, printerStream, schemaRequests, printerBidiSchemaResponses);
```

Parameters

*scriptContext*

\[在中\] [ **IPrinterScriptContext** ](https://msdn.microsoft.com/library/windows/hardware/hh768279)提供对相关的属性包的访问的对象。
*printerStream*

\[在中\] [IPrinterScriptableSequentialStream](https://msdn.microsoft.com/library/windows/hardware/hh439697)对象，它允许读取和写入访问权限的 USB 总线。
*schemaRequests*

\[在\]数组对象，其中包含的所有请求 Bidi 查询字符串。
*printerBidiSchemaResponses*

\[out\]对象脚本用来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                                                                                                             |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 已成功完成脚本。                                                                                                                                                      |
| 1            | 连接的设备未准备好提供某些请求的信息。 表示打印系统应调用再次使用在处理过程中添加任何再次查询键的函数。 |



## <a name="setschema-method"></a>setSchema 方法


此方法可处理 Bidi 设置操作。 该脚本可以确定要在设备中，设置数据，或者像清理在设备上执行某些操作的传入 Bidi 架构值墨迹的头。

如果设备未准备好处理指定的数据，该方法可以返回值为 1 以指示应在的等待时间后重试调用。

Parameters

*scriptContext*

\[在中\] [ **IPrinterScriptContext** ](https://msdn.microsoft.com/library/windows/hardware/hh768279)提供对相关的属性包的访问的对象。
*printerStream*

\[在中\] [IPrinterScriptableSequentialStream](https://msdn.microsoft.com/library/windows/hardware/hh439697)对象，它允许读取和写入访问权限的 USB 总线。
*printerBidiSchemaElement*

\[在中\] [IPrinterBidiSchemaElement](https://msdn.microsoft.com/library/windows/hardware/hh406590)对象，其中包含与要设置的 Bidi 架构值相关联的所有数据。
返回值

| 返回值 | 描述                                                                                                                                                                          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 已成功完成脚本。                                                                                                                                                   |
| 1            | 连接的设备未准备好提供某些请求的信息。 表示打印系统应调用该函数使用提供的 printerBidiSchemaElement 再次。 |



## <a name="getstatus-method"></a>getStatus 方法


此方法用于在打印设备的同时从打印机获取未经请求的状态。 仅在打印期间调用此函数。 设备应提供有关此脚本可以解释为 Bidi 架构值读取通道的数据。 由于打印数据被阻止设备的写入通道，此处被支持仅未经请求的状态。

在打印期间重复调用此方法。 应在设备将仅返回数据，如果可用且该脚本可以了解它。 如果设备不支持未经请求的状态或无需再次调用此函数，该脚本应返回值为 2，它将告知**getStatus** USBMon 成功退出中的执行线程。

Parameters

*scriptContext*

\[在中\] **IPrinterScriptContext**提供对相关的属性包的访问的对象。
*printerStream*

\[在中\] [IPrinterScriptableSequentialStream](https://msdn.microsoft.com/library/windows/hardware/hh439697)对象，它允许对 USB 总线读取访问权限。
*printerBidiSchemaResponses*

\[out\]对象脚本用来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                             |
|--------------|---------------------------------------------------------------------------------------------------------|
| 0            | 已成功完成脚本。                                                                      |
| 2            | 连接的设备不再支持未经请求的状态，不应再次调用此函数。 |



## <a name="startprintjob-method"></a>startPrintJob 方法


USBMon StartDocPort 期间调用此方法。 调用**startPrintJob**使驱动程序来修改打印流或实现基于主机的请求/响应协议，可在打印设备打印作业的同时。 作业上下文对象传递到该函数允许制造商的 JavaScript 代码来管理作业属性，并有权访问的持久的数据流。 为 JavaScript 数组的 JavaScript 代码来处理传入的打印数据。 **startPrintJob**还提供以下方面的打印机设备的访问权限：

-   通过打印流

-   通过可返回 Bidi 架构响应 USBMon 要处理的对象

语法

```javascript
function startPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

Parameters

*jobScriptContext*

\[在中\] [ **IPrinterScriptUsbJobContext** ](https://msdn.microsoft.com/library/windows/hardware/dn425143) ，制造商的 JavaScript 代码访问作业属性包和持久性数据流的对象。
*printerStream*

\[在中\] **IPrinterScriptableSequentialStream**对象，制造商的 JavaScript 代码可用于读取和写入到打印设备的数据。
*printerBidiSchemaResponses*

\[out\] [ **IPrinterBidiSchemaResponses** ](https://msdn.microsoft.com/library/windows/hardware/hh920397)对象制造商的 JavaScript 代码可以使用返回值的更改/更新的任何 Bidi 架构。

| 返回值 | 描述                                                                             |
|--------------|-----------------------------------------------------------------------------------------|
| 0            | 成功。                                                                                |
| 1            | 失败 – 清理作业上下文对象并打印后台处理程序返回错误代码。 |



## <a name="writeprintdata-method"></a>writePrintData 方法


USBMon writePort 期间调用此方法。 调用**writePrintData**使驱动程序来修改打印流或实现基于主机的请求/响应协议，可在打印设备打印作业的同时。 作业上下文对象传递到方法以允许制造商的 JavaScript 代码来管理作业属性，并有权访问的持久的数据流。 为 JavaScript 数组的 JavaScript 代码来处理传入的打印数据。 **writePrintData**还提供以下方面的打印机设备的访问权限：

-   通过打印流

-   通过可返回 Bidi 架构响应 USBMon 要处理的对象

```javascript
function writePrintData(jobScriptContext, writePrintDataProgress, printData, printerStream, printerBidiSchemaResponses);
```

Parameters

*jobScriptContext*

\[在中\] **IPrinterScriptUsbJobContext** ，制造商的 JavaScript 代码访问作业属性包和持久性数据流的对象。
*writePrintDataProgress*

\[在中\] **IPrinterScriptableSequentialStream**对象制造商的 JavaScript 代码可用于读取和写入到打印设备的数据。
*printData*

\[在中\] **IDispatch**对象，当前的打印数据的 JavaScript 数组。 *PrintData*参数允许 JavaScript 代码来操作数据到其中一个数据流中的任一缓存之前*jobScriptContext*或将其发送到打印机通过*printerStream*。
*printerStream*

\[在中\] **IPrinterScriptableSequentialStream**对象制造商的 JavaScript 代码可用于读取和写入到打印设备的数据。
*printerBidiSchemaResponses*

\[out\] **IPrinterBidiSchemaResponses**对象制造商的 JavaScript 代码可以使用返回值发生更改或更新任何 Bidi 架构。
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
<td>成功。 从打印数据流处理的字节数 (<em>printData</em>) 返回通过<em>writePrintDataProgress</em>。</td>
</tr>
<tr class="even">
<td>1</td>
<td>失败 – 到打印后台处理程序返回错误代码。</td>
</tr>
<tr class="odd">
<td>2</td>
<td><p>重试-在处理任何 Bidi 架构更新 （包括 Bidi 事件） <em>printerBidiSchemaResponses</em>，然后调用 JavaScript 函数，让制造商的代码以继续处理数据。</p>
<p>从打印数据流处理的字节数 (<em>printData</em>) 返回通过<em>writePrintDataProgress</em>。</p></td>
</tr>
<tr class="even">
<td>3</td>
<td><p>DeviceBusy – 设备通信通道不接受数据这一次。 这并不表示失败。 USBMon 应该通知后台处理程序，该设备处于繁忙状态，且然后再次在更高版本时，调用函数。</p>
<p>从打印数据流处理的字节数 (<em>printData</em>) 返回通过<em>writePrintDataProgress</em>。</p></td>
</tr>
<tr class="odd">
<td>4</td>
<td>AbortTheJob – 该设备不能继续处理作业，或用户已取消的作业使用打印设备的前面板。 当 USBMon 收到的消息中止打印作业时，它将信息传递到打印后台处理程序中止作业，然后再返回。</td>
</tr>
</tbody>
</table>



## <a name="endprintjob-method"></a>endPrintJob 方法


USBMon endDocPort 期间调用此方法。 调用**endPrintJob**使驱动程序来修改打印流或实现基于主机的请求/响应协议，可在打印设备打印作业的同时。 作业上下文对象传递到方法以允许到制造商的 JavaScript 代码：

-   完成处理保留的任何打印数据

-   访问打印流通过打印机设备

-   访问一个对象，可以传递 Bidi 架构 USBMon 要处理的响应

```javascript
function endPrintJob(jobScriptContext, printerStream, printerBidiSchemaResponses);
```

Parameters

*jobScriptContext*

\[在\]IPrinterScriptUsbJobContext，制造商的 JavaScript 代码访问作业属性包和持久性数据流的对象。
*printerStream*

\[在\]IPrinterScriptableSequentialStream 制造商的 JavaScript 代码可用于读取和写入到打印设备的数据的对象。
*printerBidiSchemaResponses*

\[out\] IPrinterBidiSchemaResponses 对象制造商的 JavaScript 代码可以使用返回值发生更改或更新任何 Bidi 架构。

| 返回值 | 描述                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0            | 成功 – 清理作业上下文对象和到打印后台处理程序返回成功。                                                                                                                                         |
| 1            | 失败 – 清理作业上下文对象并打印后台处理程序返回错误代码。                                                                                                                                   |
| 2            | 重试-在处理任何 Bidi 架构更新 （包括 Bidi 事件） *printerBidiSchemaResponses*，然后调用 JavaScript 函数，让制造商的 JavaScript 代码以继续处理数据。 |



## <a name="bidi-over-secondary-usb"></a>通过辅助 USB Bidi


如果设备支持辅助 USB 接口，则可以使用设备**getSchemas**并**setSchema**除了前面部分中所述方法**requestStatus**方法。

## <a name="requeststatus-method"></a>requestStatus 方法


此方法调用而不是**getStatus**，则**BidiUSBStatusInterface** v4 驱动程序的清单文件中指定指令。 **requestStatus**用于获取从打印设备的状态，而打印设备。

下图提供了 USB Bidi 扩展体系结构，其中显示该方案的概述其中**BidiUSBStatusInterface**指定指令和通过备用 USB 因此路由通信接口。

![usb bidi 扩展器体系结构与 requeststatus 方法](images/usbbidiext-arch2.png)

在打印期间重复调用此方法。 应在设备将仅返回数据，如果可用且该脚本可以了解它。 如果设备不支持经请求的状态或无需再次调用此方法，脚本应将返回值为 2，它将告知**getStatus** USBMon 成功退出中的执行线程。

Parameters

*scriptContext*

\[在中\] **IPrinterScriptContext**提供对相关的属性包的访问的对象。
*printerStream*

\[在中\] **IPrinterScriptableSequentialStream**对象，它允许读取和写入访问权限的 USB 总线。
*printerBidiSchemaResponses*

\[out\]对象脚本用来存储对查询密钥的所有响应。
返回值

| 返回值 | 描述                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------|
| 0            | 已成功完成脚本。                                                                    |
| 2            | 连接的设备不再支持经请求的状态，不应再次调用此函数。 |



## <a name="related-topics"></a>相关主题
[**IPrinterScriptContext**](https://msdn.microsoft.com/library/windows/hardware/hh768279)  
[IPrinterScriptableSequentialStream](https://msdn.microsoft.com/library/windows/hardware/hh439697)  
[USB Bidi 扩展程序](usb-bidi-extender.md)  



