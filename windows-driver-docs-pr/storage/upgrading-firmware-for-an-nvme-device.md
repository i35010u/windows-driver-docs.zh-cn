---
title: 升级为 NVMe 设备的固件
description: NVMe 存储设备上的固件更新颁发给该设备的微型端口驱动程序。
ms.assetid: A912715A-F82A-41E5-BE14-5B17930C29B7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0448455477b959ab6c097c77a2adfcb8ad0fa5dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390203"
---
# <a name="upgrading-firmware-for-an-nvme-device"></a>升级为 NVMe 设备的固件


NVMe 存储设备上的固件更新颁发给该设备的微型端口驱动程序。 函数用于获取固件信息的命令，下载和激活固件映像被颁发给微型端口。

## <a name="span-idfirmwareupgradeprocessspanspan-idfirmwareupgradeprocessspanspan-idfirmwareupgradeprocessspanfirmware-upgrade-process"></a><span id="Firmware_upgrade_process"></span><span id="firmware_upgrade_process"></span><span id="FIRMWARE_UPGRADE_PROCESS"></span>固件升级过程


认证 Windows NVMe 设备都能在设备处于操作更新其固件。 使用更新固件[ **IOCTL\_SCSI\_微型端口**](https://msdn.microsoft.com/library/windows/hardware/ff560512)请求 SRB 包含具有关联的固件控制数据格式。 更新过程包括：

1.  收集固件插槽信息以确定更新的放置位置。 有一些在决定固件更新所在的位置的几个注意事项。

    -   提供了多少槽？
    -   多少槽可以容纳更新？ 某些槽是只读的或保存图像，如果需要还原到以前的映像的功能，则必须保留。
    -   哪个插槽包含当前活动固件映像 （正在运行的固件）？

    若要更新设备，这就是可写和不当前处于活动状态选择槽。 在更新完成时，是覆盖选定的插槽中的所有现有图像数据。

2.  下载所选槽的新固件映像。 具体取决于图像的大小，这是图像的在单个传输操作中进行还是在连续传输的多个部分。 图像的一部分受到**最小**(*控制器最大传输大小*，512 KB)。
3.  若要下载的映像将活动固件映像，它被分配槽。 活动固件插槽切换从当前使用的槽到分配给已下载的映像的槽。 具体取决于下载和固件映像中的更改的类型，可能需要重新启动系统。 这是通过 NVMe 控制器确定。

## <a name="span-idminiportfirmwarecontrolrequestsspanspan-idminiportfirmwarecontrolrequestsspanspan-idminiportfirmwarecontrolrequestsspanminiport-firmware-control-requests"></a><span id="Miniport_firmware_control_requests"></span><span id="miniport_firmware_control_requests"></span><span id="MINIPORT_FIRMWARE_CONTROL_REQUESTS"></span>微型端口固件控制请求


在中设置每个函数命令**固件\_请求\_阻止**结构附带[ **SRB\_IO\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff566339)中的缓冲区[ **IOCTL\_SCSI\_微型端口**](https://msdn.microsoft.com/library/windows/hardware/ff560512)请求。 **ControlCode**的成员**SRB\_IO\_控制**设置为**IOCTL\_SCSI\_微型端口\_固件**表示微型端口固件操作。 函数的每个命令具有相关的信息的结构位于后**固件\_请求\_阻止**。 下表列出了每个函数命令，并包含有关系统缓冲区中的结构**IOCTL\_SCSI\_微型端口**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">输入的数据</th>
<th align="left">输出数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FIRMWARE_FUNCTION_GET_INFO</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_SLOT_INFO</p></td>
</tr>
<tr class="even">
<td align="left"><p>FIRMWARE_FUNCTION_DOWNLOAD</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_DOWNLOAD</p></td>
<td align="left"><p>SRB_IO_CONTROL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FIRMWARE_FUNCTION_ACTIVATE</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_ACTIVATE</p></td>
<td align="left"><p>SRB_IO_CONTROL</p></td>
</tr>
</tbody>
</table>

 

中定义的固件函数和关联的结构*ntddscsi.h*。

## <a name="span-idfirmwareslotinformationspanspan-idfirmwareslotinformationspanspan-idfirmwareslotinformationspanfirmware-slot-information"></a><span id="Firmware_slot_information"></span><span id="firmware_slot_information"></span><span id="FIRMWARE_SLOT_INFORMATION"></span>固件插槽信息


固件映像位置调用槽中的设备上维护。 找到可用的插槽的固件映像驻留在下载后激活时需要它。 若要查找可用的插槽，升级的实用程序可以将信息查询发送到接收槽信息描述符的设备。 下面的示例函数演示如何检索所选的 NVMe 设备上所有固件插槽的信息。

```ManagedCPlusPlus
// A device list item structure for an adapter

typedef struct _DEVICE_LIST {
    HANDLE                      Handle;
    STORAGE_ADAPTER_DESCRIPTOR  AdapterDescriptor;
} DEVICE_LIST, *PDEVICE_LIST;

BOOL
DeviceGetFirmwareInfo(
    _In_ PDEVICE_LIST DeviceList,
    _In_ DWORD        Index,
    _Inout_ PUCHAR    Buffer,
    _In_ DWORD        BufferLength,
    _In_ BOOLEAN      DisplayResult
    )
/*++

Routine Description:

    Retrieve the firmware and firmware slot information from NVMe controller.


Arguments:

    DeviceList    – a pointer to device array that contains disks information.
    Index         – the index of NVMe device in DeviceList array.
    Buffer        – a buffer for input and output.
    BufferLength  – the size of the buffer.
    DisplayResult – print information on screen or not.
  
Return Value:

    BOOLEAN

--*/
{
    BOOL    result;
    ULONG   returnedLength;
    ULONG   firmwareInfoOffset;

    PSRB_IO_CONTROL         srbControl;
    PFIRMWARE_REQUEST_BLOCK firmwareRequest;
    PSTORAGE_FIRMWARE_INFO  firmwareInfo;

    srbControl = (PSRB_IO_CONTROL)Buffer;
    firmwareRequest = (PFIRMWARE_REQUEST_BLOCK)(srbControl + 1);

    //
    // The STORAGE_FIRMWARE_INFO is located after SRB_IO_CONTROL and FIRMWARE_RESQUEST_BLOCK
    //
    firmwareInfoOffset = ((sizeof(SRB_IO_CONTROL) + sizeof(FIRMWARE_REQUEST_BLOCK) - 1) / sizeof(PVOID) + 1) * sizeof(PVOID);

    //
    // Setup the SRB control with the firmware ioctl control info
    //
    srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
    srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
    RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
    srbControl->Timeout = 30;
    srbControl->Length = BufferLength - sizeof(SRB_IO_CONTROL);

    //
    // Set firmware request fields for FIRMWARE_FUNCTION_GET_INFO. This request is to the controller so
    // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
    //
    firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
    firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
    firmwareRequest->Function = FIRMWARE_FUNCTION_GET_INFO;
    firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
    firmwareRequest->DataBufferOffset = firmwareInfoOffset;
    firmwareRequest->DataBufferLength = BufferLength - firmwareInfoOffset;

    //
    // Send the request to get the device firmware info
    //
    result = DeviceIoControl(DeviceList[Index].Handle,
                              IOCTL_SCSI_MINIPORT,
                              Buffer,
                              BufferLength,
                              Buffer,
                              BufferLength,
                              &returnedLength,
                              NULL
                              );

    //
    // Format and display the firmware info
    //
    if (DisplayResult) {
        if (!result) {
            _tprintf(_T("\t Get Firmware Information Failed: 0x%X\n"), GetLastError());
        } else {
            UCHAR   i;
            TCHAR   revision[16] = {0};

            firmwareInfo = (PSTORAGE_FIRMWARE_INFO)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

            _tprintf(_T("\t ----Firmware Information----\n"));
            _tprintf(_T("\t Support upgrade command: %s\n"), firmwareInfo->UpgradeSupport ? _T("Yes") : _T("No"));
            _tprintf(_T("\t Slot Count: %d\n"), firmwareInfo->SlotCount);
            _tprintf(_T("\t Current Active Slot: %d\n"), firmwareInfo->ActiveSlot);

            if (firmwareInfo->PendingActivateSlot == STORAGE_FIRMWARE_INFO_INVALID_SLOT) {
                _tprintf(_T("\t Pending Active Slot: %s\n\n"),  _T("No"));
            } else {
                _tprintf(_T("\t Pending Active Slot: %d\n\n"), firmwareInfo->PendingActivateSlot);
            }

            for (i = 0; i < firmwareInfo->SlotCount; i++) {
                RtlCopyMemory(revision, &firmwareInfo->Slot[i].Revision.AsUlonglong, 8);

                _tprintf(_T("\t\t Slot Number: %d\n"), firmwareInfo->Slot[i].SlotNumber);
                _tprintf(_T("\t\t Slot Read Only: %s\n"), firmwareInfo->Slot[i].ReadOnly ? _T("Yes") : _T("No"));
                _tprintf(_T("\t\t Revision: %s\n"), revision);
                _tprintf(_T("\n"));
            }
        }

        _tprintf(_T("\n"));
    }

    return result;
}
```

在一个数组中返回槽信息**存储\_固件\_槽\_信息**结构。 每个结构指示激活状态和固件插槽的可用性。 有关可用性的条件有：

-   **ReadOnly**成员设置为 0。
-   槽不是由槽编号中的活动槽**ActiveSlot**的成员**存储\_固件\_信息**。
-   **PendingActiveSlot**的成员**存储\_固件\_信息**设置为存储\_固件\_信息\_无效\_槽。
-   **PendingActiveSlot**的成员**存储\_固件\_信息**未设置为所需的槽。

此外，如果在槽状态符合可用性的条件，但**信息**字符串包含有效的修订的数据，为非零字节，则插槽包含有效的固件映像，但它可能被替换。 所有零**信息**字符串指示一个空插槽。

## <a name="span-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanspan-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanspan-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanexample-firmware-upgrade---slot-selection-download-and-activation"></a><span id="Example__Firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="example__firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="EXAMPLE__FIRMWARE_UPGRADE_-_SLOT_SELECTION__DOWNLOAD__AND_ACTIVATION"></span>示例：固件升级-所选槽、 下载和激活


升级的实用程序将执行前面所述更新固件控制器中的三个步骤。 例如，以下升级例程包含代码过程中的每个步骤。 槽发现步骤，所示*DeviceGetFirmwareInfo*示例中，调用通过升级例程，以选择可用的插槽。 紧接所选槽演示图像下载和激活步骤。 在每个步骤，显示相应函数命令的使用。

在下载步骤中，固件图像文件读取到的分配的缓冲区和缓冲区的内容传输到控制器。 如果固件图像文件大小大于缓冲区的大小，图像文件读取多个时间，固件映像的该部分传输直到读取整个文件。

在的固件映像下载完成之后，激活步骤需要从控制器的两个操作。 首先，将选定的插槽分配给固件映像，并且第二，所选的槽设置为活动的槽。

```ManagedCPlusPlus
VOID
DeviceFirmwareUpgrade(
    _In_ PDEVICE_LIST DeviceList,
    _In_ DWORD        Index,
    _In_ TCHAR*       FileName
    )
/*++

Routine Description:

    Performs a firmware upgrade to the NVMe controller. The an available firmware
    slot is selected, the firmware is downloaded to the controller from an image
    file, and the new firmware is activated.


Arguments:

    DeviceList    – a pointer to device array that contains disks information.
    Index         – the index of NVMe device in DeviceList array.
    FileName      – the name of the firmware upgrade image file.
  
Return Value:

    None

--*/
{
    BOOL                    result;
    PUCHAR                  buffer = NULL;
    ULONG                   bufferSize;
    ULONG                   firmwareStructureOffset;
    ULONG                   imageBufferLength;

    PSRB_IO_CONTROL         srbControl;
    PFIRMWARE_REQUEST_BLOCK firmwareRequest;

    PSTORAGE_FIRMWARE_INFO      firmwareInfo;
    PSTORAGE_FIRMWARE_DOWNLOAD  firmwareDownload;
    PSTORAGE_FIRMWARE_ACTIVATE  firmwareActivate;

    ULONG                   slotNumber;
    ULONG                   returnedLength;
    ULONG                   i;

    HANDLE                  fileHandle = NULL;
    ULONG                   imageOffset;
    ULONG                   readLength;
    BOOLEAN                 moreToDownload;

    //
    // The STORAGE_FIRMWARE_INFO is located after SRB_IO_CONTROL and FIRMWARE_RESQUEST_BLOCK
    //
    firmwareStructureOffset = ((sizeof(SRB_IO_CONTROL) + sizeof(FIRMWARE_REQUEST_BLOCK) - 1) / sizeof(PVOID) + 1) * sizeof(PVOID);

    //
    // The Max Transfer Length limits the part of buffer that may need to transfer to controller, not the whole buffer.
    //
    bufferSize = min(DeviceList[Index].AdapterDescriptor.MaximumTransferLength, 2 * 1024 * 1024);
    bufferSize += firmwareStructureOffset;
    bufferSize += FIELD_OFFSET(STORAGE_FIRMWARE_DOWNLOAD, ImageBuffer);

    buffer = (PUCHAR)malloc(bufferSize);
    if (buffer == NULL) {
        _tprintf(_T("\t FirmwareUpgrade - Allocate buffer failed: 0x%X\n"), GetLastError());
        return;
    }

    //
    // calculate the space available for the firmware image portion of the buffer allocation
    // 
    imageBufferLength = bufferSize - firmwareStructureOffset - sizeof(STORAGE_FIRMWARE_DOWNLOAD);

    RtlZeroMemory(buffer, bufferSize);

    // ---------------------------------------------------------------------------
    // ( 1 ) SELECT A SUITABLE FIRMWARE SLOT
    // ---------------------------------------------------------------------------

    //
    // Get firmware slot information data.
    //
    result = DeviceGetFirmwareInfo(DeviceList, Index, buffer, bufferSize, FALSE);

    if (result == FALSE) {
        _tprintf(_T("\t FirmwareUpgrade: Get Firmware Information Failed: 0x%X\n"), GetLastError());
        goto Exit;
    }

    //
    // Set the request structure pointers
                //
    srbControl = (PSRB_IO_CONTROL)buffer;
    firmwareRequest = (PFIRMWARE_REQUEST_BLOCK)(srbControl + 1);
    firmwareInfo = (PSTORAGE_FIRMWARE_INFO)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

    if (srbControl->ReturnCode != FIRMWARE_STATUS_SUCCESS) {
        _tprintf(_T("\t FirmwareUpgrade - get firmware info failed. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        goto Exit;
    }

    //
    // SelectFind the first writable slot.
    //
    slotNumber = (ULONG)-1;

    if (firmwareInfo->UpgradeSupport) {
        for (i = 0; i < firmwareInfo->SlotCount; i++) {
            if (firmwareInfo->Slot[i].ReadOnly == FALSE) {
                slotNumber = firmwareInfo->Slot[i].SlotNumber;
                break;
            }
        }
    }

    //
    // If no writable slot is found, bypass downloading and activation
    //
    if (slotNumber == (ULONG)-1) {
        _tprintf(_T("\t FirmwareUpgrade - No writable Firmware slot.\n"));
        goto Exit;
    }

    // ---------------------------------------------------------------------------
    // ( 2 ) DOWNLOAD THE FIRMWARE IMAGE TO THE CONTROLLER
    // ---------------------------------------------------------------------------

    //
    // initialize image length and offset
    //
    imageBufferLength = (imageBufferLength / sizeof(PVOID)) * sizeof(PVOID);
    imageOffset = 0;
    readLength = 0;
    moreToDownload = TRUE;

    //
    // Open image file and download it to controller.
    //
    if (FileName == NULL) {
        _tprintf(_T("\t FirmwareUpgrade - No firmware file specified.\n"));
        goto Exit;
    }

    fileHandle = CreateFile(FileName,              // file to open
                            GENERIC_READ,          // open for reading
                            FILE_SHARE_READ,       // share for reading
                            NULL,                  // default security
                            OPEN_EXISTING,         // existing file only
                            FILE_ATTRIBUTE_NORMAL, // normal file
                            NULL);                 // no attr. template

    if (fileHandle == INVALID_HANDLE_VALUE) {
        _tprintf(_T("\t FirmwareUpgrade - unable to open file \"%s\" for read.\n"), FileName);
        goto Exit;
    }

    //
    // Read and download the firmware from the image file into image buffer length portions. Send the
    // image portion to the controller.
    //
    while (moreToDownload) {

        RtlZeroMemory(buffer, bufferSize);

        //
        // Setup the SRB control with the firmware ioctl control info
        //
        srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
        srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
        RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
        srbControl->Timeout = 30;
        srbControl->Length = bufferSize - sizeof(SRB_IO_CONTROL);

        //
        // Set firmware request fields for FIRMWARE_FUNCTION_DOWNLOAD. This request is to the controller so
        // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
        //
        firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
        firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
        firmwareRequest->Function = FIRMWARE_FUNCTION_DOWNLOAD;
        firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
        firmwareRequest->DataBufferOffset = firmwareStructureOffset;
        firmwareRequest->DataBufferLength = bufferSize - firmwareStructureOffset;

        //
        // Initialize the firmware data buffer pointer to the proper position after the request structure
        //
        firmwareDownload = (PSTORAGE_FIRMWARE_DOWNLOAD)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

        if (ReadFile(fileHandle, firmwareDownload->ImageBuffer, imageBufferLength, &readLength, NULL) == FALSE) {
            _tprintf(_T("\t FirmwareUpgrade - Read firmware file failed.\n"));
            goto Exit;
        }

        if (readLength == 0) {
            moreToDownload = FALSE;
            break;
        }

        if ((readLength % sizeof(ULONG)) != 0) {
            _tprintf(_T("\t FirmwareUpgrade - Read firmware file failed.\n"));
        }

        //
        // Set the download parameters and adjust the offset for this portion of the firmware image
        //
        firmwareDownload->Version = 1;
        firmwareDownload->Size = sizeof(STORAGE_FIRMWARE_DOWNLOAD);
        firmwareDownload->Offset = imageOffset;
        firmwareDownload->BufferSize = readLength;

        //
        // download this portion of firmware to the device
        //
        result = DeviceIoControl(DeviceList[Index].Handle,
                                 IOCTL_SCSI_MINIPORT,
                                 buffer,
                                 bufferSize,
                                 buffer,
                                 bufferSize,
                                 &returnedLength,
                                 NULL
                                 );

        if (result == FALSE) {
            _tprintf(_T("\t FirmwareUpgrade - IOCTL - firmware download failed. 0x%X.\n"), GetLastError());
            goto Exit;
        }

        if (srbControl->ReturnCode != FIRMWARE_STATUS_SUCCESS) {
            _tprintf(_T("\t FirmwareUpgrade - firmware download failed. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
            goto Exit;
        }

        //
        // Update Image Offset for next iteration.
        //
        imageOffset += readLength;
    }

    // ---------------------------------------------------------------------------
    // ( 3 ) ACTIVATE THE FIRMWARE SLOT ASSIGNED TO THE UPGRADE
    // ---------------------------------------------------------------------------

    //
    // Activate the newly downloaded image with the assigned slot.
    //
    RtlZeroMemory(buffer, bufferSize);

    //
    // Setup the SRB control with the firmware ioctl control info
    //
    srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
    srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
    RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
    srbControl->Timeout = 30;
    srbControl->Length = bufferSize - sizeof(SRB_IO_CONTROL);

    //
    // Set firmware request fields for FIRMWARE_FUNCTION_ACTIVATE. This request is to the controller so
    // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
    //
    firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
    firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
    firmwareRequest->Function = FIRMWARE_FUNCTION_ACTIVATE;
    firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
    firmwareRequest->DataBufferOffset = firmwareStructureOffset;
    firmwareRequest->DataBufferLength = bufferSize - firmwareStructureOffset;

    //
    // Initialize the firmware activation structure pointer to the proper position after the request structure
    //
    firmwareActivate = (PSTORAGE_FIRMWARE_ACTIVATE)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

    //
    // Set the activation parameters with the available slot selected
    //
    firmwareActivate->Version = 1;
    firmwareActivate->Size = sizeof(STORAGE_FIRMWARE_ACTIVATE);
    firmwareActivate->SlotToActivate = (UCHAR)slotNumber;

    //
    // Send the activation request
    //
    result = DeviceIoControl(DeviceList[Index].Handle,
                                IOCTL_SCSI_MINIPORT,
                                buffer,
                                bufferSize,
                                buffer,
                                bufferSize,
                                &returnedLength,
                                NULL
                                );


    if (result == FALSE) {
        _tprintf(_T("\t FirmwareUpgrade - IOCTL - firmware activate failed. 0x%X.\n"), GetLastError());
        goto Exit;
    }

    //
    // Display status result from firmware activation
    //
    switch (srbControl->ReturnCode) {
    case FIRMWARE_STATUS_SUCCESS:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate succeeded.\n"));
        break;

    case FIRMWARE_STATUS_POWER_CYCLE_REQUIRED:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate succeeded. PLEASE REBOOT COMPUTER.\n"));
        break;

    case FIRMWARE_STATUS_ILLEGAL_REQUEST:
    case FIRMWARE_STATUS_INVALID_PARAMETER:
    case FIRMWARE_STATUS_INPUT_BUFFER_TOO_BIG:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate parameter error. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        break;

    case FIRMWARE_STATUS_INVALID_SLOT:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, slot number invalid.\n"));
        break;

    case FIRMWARE_STATUS_INVALID_IMAGE:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, invalid firmware image.\n"));
        break;

    case FIRMWARE_STATUS_ERROR:
    case FIRMWARE_STATUS_CONTROLLER_ERROR:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, error returned.\n"));
        break;

    default:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, unexpected error. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        break;
   }

Exit:

    if (fileHandle != NULL) {
        CloseHandle(fileHandle);
    }

    if (buffer != NULL) {
        free(buffer);
    }

    return;
}
```

**请注意**  不支持同时下载多个固件映像。 单个固件下载始终后跟单个固件激活。

 

通过使用相应的槽数只需激活函数命令，可以重新激活已驻留在槽中的固件映像。

**IOCTL\_SCSI\_微型端口\_固件**SRB I/O 控制的控制代码是从 Windows 8.1 开始提供。

 

 




