---
title: 供应商扩展的命令
description: 供应商扩展的命令
ms.assetid: 3d360a9f-5a65-452b-a8ad-080dc7d8c8f5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 300cd6c53b26ade72f2bbfca44d0014f6c855193
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375388"
---
# <a name="vendor-extended-commands"></a>供应商扩展的命令





应用程序可以将任意命令发送到通过设备**IWiaItemExtras::Escape**方法，Microsoft Windows SDK 文档中所述。 通过调用**QueryInterface**上的根项目，可以检索一个指向**IWiaItemExtras**接口。 然后，应用程序可以构造 PTP 命令使用的任何操作码和参数，并将此命令发送到设备。 应用程序还可以将数据发送到或从设备接收数据。

设备通知操作的结果的应用程序时**IWiaItemExtras::Escape**方法返回时，在响应代码和响应中的参数填写[ **PTP\_供应商\_数据\_出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ptpusd/ns-ptpusd-_ptp_vendor_data_out)结构。 **SessionId**并**TransactionId**的成员[ **PTP\_供应商\_数据\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ptpusd/ns-ptpusd-_ptp_vendor_data_in)结构将被忽略。 驱动程序提供这些正确的值。

为非转义的供应商定义命令\_PTP\_清除\_将停止，特殊的标志，转义\_PTP\_供应商\_命令，必须 （使用 OR 运算符） 组合使用命令在中使用**IWiaItemExtras::Escape**方法。 如果供应商定义的命令创建或删除使用以下所述的标志的设备上的对象，该驱动程序添加或从其内部结构中删除对象并生成 WIA 事件。 应通过适当的 WIA 接口发出其他标准的所有命令。

第一个参数**IWiaItemExtras::Escape**是一个或多个下列标志的组合：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>转义码</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_CMD</p></td>
<td><p>正在添加对象并且该对象的句柄在一个命令参数。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_CMD</p></td>
<td><p>正在删除对象并且该对象的句柄在一个命令参数。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_RESP</p></td>
<td><p>正在添加对象并且该对象的句柄在一个响应参数。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_RESP</p></td>
<td><p>正在删除对象并且该对象的句柄在一个响应参数。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM1</p></td>
<td><p>添加或删除对象的句柄是命令或响应的第一个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM2</p></td>
<td><p>添加或删除对象的句柄是命令或响应的第二个参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM3</p></td>
<td><p>添加或删除对象的句柄是命令或响应的第三个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM4</p></td>
<td><p>添加或删除对象的句柄是命令或响应的第四个参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM5</p></td>
<td><p>添加或删除对象的句柄是命令或响应的第五个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_CLEAR_STALLS</p></td>
<td><p>清除任何供应商扩展的命令导致的错误情况。 此标志不能与任何其他标志结合使用。 有关此标志的详细信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_VENDOR_COMMAND</p></td>
<td><p>命令为供应商扩展的命令。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  当应用程序调用**IWiaItemExtras::Escape**通过转义符\_PTP\_清除\_停滞标记此方法的第一个参数为驱动程序发出 PTP**获取设备状态**请求以确定任何终结点是否处于停滞状态。 如果**获取设备状态**命令将成功，驱动程序问题[ **IOCTL\_重置\_管道**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_reset_pipe) USB 控制代码的每个此类终结点。 如果**获取设备状态**命令将会失败，驱动程序将发出 PTP**设备重置**请求。 **获取设备状态**并**设备重置**PIMA 15740:2000 标准，第一版和 USB 仍图像捕获设备定义的 (USB SICDD) 的修订版本 1.0 中描述了。

 

下面的示例代码说明了如何使用供应商扩展命令接口。 确保你的代码，包括*ptpusd.h*标头，因为它包含转义代码和其他常量的定义并[ **PTP\_供应商\_数据\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ptpusd/ns-ptpusd-_ptp_vendor_data_in)并[ **PTP\_供应商\_数据\_出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ptpusd/ns-ptpusd-_ptp_vendor_data_out)结构。 **IWiaItemExtras**接口通过使用调用**QueryInterface**根项。 指向该项根*pIWiaRootItem*，可以获取，例如，通过调用**IWiaDevMgr::SelectDeviceDlg** （Microsoft Windows SDK 文档中所述）。

```cpp
//
// Test IWiaItemExtras::Escape method
//
HRESULT hr = S_OK;
IWiaItemExtras *pIWiaItemExtras = NULL;

hr = pIWiaRootItem->QueryInterface(IID_IWiaItemExtras,
                                   (VOID **) &pIWiaItemExtras);
if (FAILED(hr)) {
    MessageBox("QueryInterface for IWiaItemExtras failed");
    return;
}

PTP_VENDOR_DATA_IN *pDataIn = NULL;
PTP_VENDOR_DATA_OUT *pDataOut = NULL;
DWORD dwDataInSize = SIZEOF_REQUIRED_VENDOR_DATA_IN;
DWORD dwDataOutSize = SIZEOF_REQUIRED_VENDOR_DATA_OUT + 0x1000;
DWORD dwActualDataOutSize = 0;

pDataIn = (PTP_VENDOR_DATA_IN *) CoTaskMemAlloc(dwDataInSize);
if (!pDataIn) {
    MessageBox("CoTaskMemAlloc failed");
    return;
}

pDataOut = (PTP_VENDOR_DATA_OUT *) CoTaskMemAlloc(dwDataOutSize);
if (!pDataOut) {
 CoTaskMemFree(pDataIn);
    MessageBox("CoTaskMemAlloc failed");
    return;
}
ZeroMemory(pDataIn, dwDataInSize);
ZeroMemory(pDataOut, dwDataOutSize);

pDataIn->OpCode = 0x1001;
pDataIn->SessionId = 0;     // The driver will fill this in.
pDataIn->TransactionId = 0; // The driver will fill this in.
pDataIn->NumParams = 0;

//
// pDataIn->NextPhase informs the PTP driver whether to 
// read data from the device (as shown), or
// write data to the device (use PTP_NEXTPHASE_WRITE_DATA),
// to neither read nor write data (use PTP_NEXTPHASE_NO_DATA).
//
pDataIn->NextPhase = PTP_NEXTPHASE_READ_DATA;

hr = pIWiaItemExtras->Escape(ESCAPE_PTP_VENDOR_COMMAND,
                             (BYTE *) pDataIn, dwDataInSize,
                             (BYTE *) pDataOut, dwDataOutSize,
                             &dwActualDataOutSize);

if (FAILED(hr)) {
    MessageBox("Escape failed");
    return;
}

//
// Data returned from device is located at pDataOut->VendorReadData.
//
```

 

 




