---
title: 如何实现扩展的相机控件属性
description: 实现照相机驱动程序的扩展相机控件属性。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86a2874881780ce2e78d4d25878f11dd41126473
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830867"
---
# <a name="how-to-implement-extended-camera-control-properties"></a>如何实现扩展的相机控件属性


照相机驱动程序应将 [扩展相机控制属性](extended-camera-control-properties.md) 作为单个属性集实现，也就是说，每个属性都应作为单个属性集来实现。 下面的示例代码可用作实现这些属性的起点。

**注意**  由于扩展属性的数据大小可以是任意长度，因此通过传递 null 缓冲区来查询用户模式堆栈的数据大小。 需要两步过程：首先，驱动程序返回所需的长度（如示例代码所示），然后用户模式堆栈为属性数据请求适当的缓冲区。

 

## <a name="driver-implementation"></a>驱动程序实现


```cpp
DEFINE_KSPROPERTY_TABLE(SocSimFilterFocusPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FocusRectHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FocusRectHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterVideoStabPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::VideoStabilizationModeHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_TABLE(SocSimFilterFlashPropertyItems)
{       
    DEFINE_KSPROPERTY_ITEM(
        0,
        CCaptureFilter::FlashHandler,
        sizeof(KSPROPERTY),
        0,
        CCaptureFilter::FlashHandler,
        NULL, 0, NULL, NULL, 0
        )
};

DEFINE_KSPROPERTY_SET_TABLE(SocSimFilterPropertySets)
{
    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_REGION_OF_INTEREST,
        SIZEOF_ARRAY(SocSimFilterFocusPropertyItems),
        SocSimFilterFocusPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_FLASH,
        SIZEOF_ARRAY(SocSimFilterFlashPropertyItems),
        SocSimFilterFlashPropertyItems,
        0,
        NULL),

    DEFINE_KSPROPERTY_SET(
        &PROPSETID_VIDCAP_CAMERACONTROL_VIDEO_STABILIZATION,
        SIZEOF_ARRAY(SocSimFilterVideoStabPropertyItems),
        SocSimFilterVideoStabPropertyItems,
        0,
        NULL)

};

NTSTATUS
CCaptureFilter::FlashHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFilter->m_Flash = pFlash->Flash;
            pFilter->m_FlashCapabilites = pFlash->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S))
        {
            PKSPROPERTY_CAMERACONTROL_FLASH_S pFlash = (PKSPROPERTY_CAMERACONTROL_FLASH_S)pData;
            pFlash->Flash = pFilter->m_Flash;
            pFlash->Capabilities = pFilter->m_FlashCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_FLASH_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::VideoStabilizationModeHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pFilter->m_VideoStabMode = pVideoStab->VideoStabilizationMode;
            pFilter->m_VideoStabCapabilites = pVideoStab->Capabilities;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S))
        {
            PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S pVideoStab = (PKSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S)pData;
            pVideoStab->VideoStabilizationMode = pFilter->m_VideoStabMode;
            pVideoStab->Capabilities = pFilter->m_VideoStabCapabilites;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_VIDEOSTABILIZATION_MODE_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}

NTSTATUS
CCaptureFilter::FocusRectHandler(
    __in    PIRP Irp,
    __in    PKSPROPERTY Property,
    __inout PVOID pData
    )
{
    PAGED_CODE();
    NTSTATUS Status = STATUS_SUCCESS;
    NT_ASSERT(Irp);
    NT_ASSERT(Property);

    CCaptureFilter* pFilter = reinterpret_cast <CCaptureFilter*>(KsGetFilterFromIrp(Irp)->Context);

    PIO_STACK_LOCATION pIrpStack = IoGetCurrentIrpStackLocation(Irp);
    ULONG ulOutputBufferLength = pIrpStack->Parameters.DeviceIoControl.OutputBufferLength;
    ULONG InputBufferLength = pIrpStack->Parameters.DeviceIoControl.InputBufferLength;

    if (Property->Flags & KSPROPERTY_TYPE_SET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFilter->m_FocusRect.left = pFocusRect->FocusRect.left;
            pFilter->m_FocusRect.top = pFocusRect->FocusRect.top;
            pFilter->m_FocusRect.right = pFocusRect->FocusRect.right;
            pFilter->m_FocusRect.bottom = pFocusRect->FocusRect.bottom;
            pFilter->m_AutoFocusLock = pFocusRect->AutoFocusLock;
            pFilter->m_AutoExposureLock = pFocusRect->AutoExposureLock;
            pFilter->m_AutoWhitebalanceLock = pFocusRect->AutoWhitebalanceLock;
            Status = STATUS_SUCCESS;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
        }
        else 
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }
    else if (Property->Flags & KSPROPERTY_TYPE_GET)
    {
        if (ulOutputBufferLength == 0)
        {
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_BUFFER_OVERFLOW;
        }
        else if (ulOutputBufferLength < sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            Status = STATUS_BUFFER_TOO_SMALL;
        }
        else if (pData && ulOutputBufferLength >= sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S))
        {
            PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S pFocusRect = (PKSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S)pData;
            pFocusRect->FocusRect.left = pFilter->m_FocusRect.left;
            pFocusRect->FocusRect.top = pFilter->m_FocusRect.top;
            pFocusRect->FocusRect.right = pFilter->m_FocusRect.right;
            pFocusRect->FocusRect.bottom = pFilter->m_FocusRect.bottom;
            pFocusRect->AutoFocusLock = pFilter->m_AutoFocusLock;
            pFocusRect->AutoExposureLock = pFilter->m_AutoExposureLock;
            pFocusRect->AutoWhitebalanceLock = pFilter->m_AutoWhitebalanceLock;
            Irp->IoStatus.Information = sizeof(KSPROPERTY_CAMERACONTROL_REGION_OF_INTEREST_S);
            Status = STATUS_SUCCESS;
        }
        else
        {
            Status = STATUS_INVALID_PARAMETER;
        }
    }

    return Status;
}
```

 

 




