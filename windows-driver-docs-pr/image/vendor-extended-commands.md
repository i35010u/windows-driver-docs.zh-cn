---
title: 供应商扩展命令
description: 供应商扩展命令
ms.assetid: 3d360a9f-5a65-452b-a8ad-080dc7d8c8f5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a53ae7a1f478a068540fe8cbf4a1d46086e5e9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840725"
---
# <a name="vendor-extended-commands"></a>供应商扩展命令





应用程序可以通过**IWiaItemExtras：： Escape**方法将任意命令发送到设备，该方法在 Microsoft Windows SDK 文档中进行了介绍。 通过对根项调用**QueryInterface** ，可以检索指向**IWiaItemExtras**接口的指针。 然后，应用程序可以使用任何操作码和参数构造 PTP 命令，并将此命令发送到设备。 应用程序还可以将数据发送到设备或从设备接收数据。

当**IWiaItemExtras：： Escape**方法返回时，该设备将通知应用程序的结果，并在[**PTP\_供应商\_数据\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_out)结构中填充响应代码和响应参数。 将忽略[**PTP\_供应商\_数据\_结构中**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_in)的**SessionId**和**TransactionId**成员。 驱动程序为这些值提供正确的值。

对于除 ESCAPE\_PTP 以外的供应商定义的命令\_清楚\_停止项，必须使用 IWiaItemExtras 中使用的命令组合（使用 OR 运算符）的特殊\_\_标志（使用 OR 运算符） **：： Escape**方法。\_ 如果供应商定义的命令使用以下所述标志在设备上创建或删除对象，则驱动程序会在其内部结构中添加或删除对象，并生成 WIA 事件。 所有其他标准命令都应该通过适当的 WIA 接口发出。

**IWiaItemExtras：： Escape**的第一个参数是以下一个或多个标志的组合：

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
<td><p>正在添加一个对象，并且该对象的句柄位于其中一个命令参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_CMD</p></td>
<td><p>正在删除对象，并且该对象的句柄位于其中一个命令参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADD_OBJ_RESP</p></td>
<td><p>正在添加一个对象，并且该对象的句柄位于其中一个响应参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_REM_OBJ_RESP</p></td>
<td><p>正在删除对象，并且该对象的句柄位于其中一个响应参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM1</p></td>
<td><p>添加或删除的对象的句柄位于命令或响应的第一个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM2</p></td>
<td><p>添加或删除的对象的句柄位于命令或响应的第二个参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM3</p></td>
<td><p>添加或删除的对象的句柄位于命令或响应的第三个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_ADDREM_PARM4</p></td>
<td><p>添加或删除的对象的句柄位于命令或响应的第四个参数中。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_ADDREM_PARM5</p></td>
<td><p>添加或删除的对象的句柄位于命令或响应的第五个参数中。</p></td>
</tr>
<tr class="even">
<td><p>ESCAPE_PTP_CLEAR_STALLS</p></td>
<td><p>清除由供应商扩展命令引起的任何错误条件。 此标志不能与任何其他标志结合使用。 有关此标志的详细信息，请参阅此表后面的说明。</p></td>
</tr>
<tr class="odd">
<td><p>ESCAPE_PTP_VENDOR_COMMAND</p></td>
<td><p>命令是一个供应商扩展的命令。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   当应用程序使用转义\_PTP 调用**IWiaItemExtras：： escape**\_清除\_隔间标志作为此方法的第一个参数时，驱动程序会将 PTP**获取设备状态**请求发送到确定是否有任何终结点处于卡住状态。 如果 "**获取设备状态**" 命令成功，则驱动程序将发出[**IOCTL\_重置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbscan/ni-usbscan-ioctl_reset_pipe)每个此类终结点\_管道 USB 控制代码。 如果 "**获取设备状态**" 命令失败，则驱动程序会发出 PTP**设备重置**请求。 **获取设备状态**和**设备重置**的说明，请参阅 Usb 静止映像捕获设备定义的 pima indian diabetes 15740:2000 标准版、第一版和修订版本1.0 （usb SICDD）。

 

下面的示例代码演示如何使用供应商扩展的命令界面。 请确保您的代码包括*ptpusd*标头，因为它包含转义码和其他常量的定义，而[**PTP\_供应商\_数据\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_in)和[**PTP\_供应商\_数据\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ptpusd/ns-ptpusd-_ptp_vendor_data_out)结构。 使用对根项的**QueryInterface**的调用来获取**IWiaItemExtras**接口。 可以通过调用**IWiaDevMgr：： SelectDeviceDlg** （如 Microsoft Windows SDK 文档中所述）来获取指向此根项（ *pIWiaRootItem*）的指针。

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

 

 




