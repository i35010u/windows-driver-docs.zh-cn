---
title: 返回 NSTATUS 代码的 KMDF 函数
description: 返回 NSTATUS 代码的 KMDF 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0420b2fac4e298321f92bdacf444580b24d86b14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823309"
---
# <a name="kmdf-functions-that-return-nstatus-codes"></a>返回 NSTATUS 代码的 KMDF 函数


下面是返回 NTSTATUS 代码的 KMDF DDIs 的列表。 其中的任何 DDIs 可能会失败，但以下两种情况除外： **WdfRequestReuse** 和 **WdfWaitLockAcquire**。

**WdfChildListAddOrUpdateChildDescriptionAsPresent**

**WdfChildListCreate**

**WdfChildListRetrieveAddressDescription**

**WdfChildListRetrieveNextDevice**

**WdfChildListUpdateChildDescriptionAsMissing**

**WdfCmResourceListAppendDescriptor**

**WdfCmResourceListInsertDescriptor**

**WdfCollectionAdd**

**WdfCollectionCreate**

**WdfCommonBufferCreate**

**WdfCommonBufferCreateWithConfig**

**WdfDeviceAddDependentUsageDeviceObject**

**WdfDeviceAddQueryInterface**

**WdfDeviceAddRemovalRelationsPhysicalDevice**

**WdfDeviceAllocAndQueryProperty**

**WdfDeviceAssignMofResourceName**

**WdfDeviceAssignS0IdleSettings**

**WdfDeviceAssignSxWakeSettings**

**WdfDeviceConfigureRequestDispatching**

**WdfDeviceCreate**

**WdfDeviceCreateDeviceInterface**

**WdfDeviceCreateSymbolicLink**

**WdfDeviceEnqueueRequest**

**WdfDeviceIndicateWakeStatus**

**WdfDeviceInitAssignName**

**WdfDeviceInitAssignSDDLString**

**WdfDeviceInitAssignWdmIrpPreprocessCallback**

**WdfDeviceInitRegisterPnpStateChangeCallback**

**WdfDeviceInitRegisterPowerPolicyStateChangeCallback**

**WdfDeviceInitRegisterPowerStateChangeCallback**

**WdfDeviceMiniportCreate**

**WdfDeviceOpenRegistryKey**

**WdfDeviceQueryProperty**

**WdfDeviceRetrieveDeviceInterfaceString**

**WdfDeviceRetrieveDeviceName**

**WdfDeviceStopIdle**

**WdfDeviceWdmDispatchPreprocessedIrp**

**WdfDmaEnablerCreate**

**WdfDmaTransactionCreate**

**WdfDmaTransactionExecute**

**WdfDmaTransactionInitialize**

**WdfDmaTransactionInitializeUsingRequest**

**WdfDmaTransactionRelease**

**WdfDpcCreate**

**WdfDriverCreate**

**WdfDriverOpenParametersRegistryKey**

**WdfDriverRegisterTraceInfo**

**WdfDriverRetrieveVersionString**

**WdfFdoAddStaticChild**

**WdfFdoInitAllocAndQueryProperty**

**WdfFdoInitOpenRegistryKey**

**WdfFdoInitQueryProperty**

**WdfFdoQueryForInterface**

**WdfInterruptCreate**

**WdfIoQueueCreate**

**WdfIoQueueFindRequest**

**WdfIoQueueReadyNotify**

**WdfIoQueueRetrieveFoundRequest**

**WdfIoQueueRetrieveNextRequest**

**WdfIoQueueRetrieveRequestByFileObject**

**WdfIoResourceListAppendDescriptor**

**WdfIoResourceListCreate**

**WdfIoResourceListInsertDescriptor**

**WdfIoResourceRequirementsListAppendIoResList**

**WdfIoResourceRequirementsListInsertIoResList**

**WdfIoTargetAllocAndQueryTargetProperty**

**WdfIoTargetCreate**

**WdfIoTargetFormatRequestForInternalIoctl**

**WdfIoTargetFormatRequestForInternalIoctlOthers**

**WdfIoTargetFormatRequestForIoctl**

**WdfIoTargetFormatRequestForRead**

**WdfIoTargetFormatRequestForWrite**

**WdfIoTargetOpen**

**WdfIoTargetQueryForInterface**

**WdfIoTargetQueryTargetProperty**

**WdfIoTargetSendInternalIoctlOthersSynchronously**

**WdfIoTargetSendInternalIoctlSynchronously**

**WdfIoTargetSendIoctlSynchronously**

**WdfIoTargetSendReadSynchronously**

**WdfIoTargetSendWriteSynchronously**

**WdfIoTargetStart**

**WdfLookasideListCreate**

**WdfMemoryAssignBuffer**

**WdfMemoryCopyFromBuffer**

**WdfMemoryCopyToBuffer**

**WdfMemoryCreate**

**WdfMemoryCreateFromLookaside**

**WdfMemoryCreatePreallocated**

**WdfObjectAllocateContext**

**WdfObjectCreate**

**WdfObjectQuery**

**WdfPdoAddEjectionRelationsPhysicalDevice**

**WdfPdoInitAddCompatibleID**

**WdfPdoInitAddDeviceText**

**WdfPdoInitAddHardwareID**

**WdfPdoInitAssignDeviceID**

**WdfPdoInitAssignInstanceID**

**WdfPdoInitAssignRawDevice**

**WdfPdoMarkMissing**

**WdfPdoRetrieveAddressDescription**

**WdfPdoRetrieveIdentificationDescription**

**WdfPdoUpdateAddressDescription**

**WdfRegistryAssignMemory**

**WdfRegistryAssignMultiString**

**WdfRegistryAssignString**

**WdfRegistryAssignULong**

**WdfRegistryAssignUnicodeString**

**WdfRegistryAssignValue**

**WdfRegistryCreateKey**

**WdfRegistryOpenKey**

**WdfRegistryQueryMemory**

**WdfRegistryQueryMultiString**

**WdfRegistryQueryString**

**WdfRegistryQueryULong**

**WdfRegistryQueryUnicodeString**

**WdfRegistryQueryValue**

**WdfRegistryRemoveKey**

**WdfRegistryRemoveValue**

**WdfRequestAllocateTimer**

**WdfRequestChangeTarget**

**WdfRequestCreate**

**WdfRequestCreateFromIrp**

**WdfRequestForwardToIoQueue**

**WdfRequestGetStatus**

**WdfRequestProbeAndLockUserBufferForRead**

**WdfRequestProbeAndLockUserBufferForWrite**

**WdfRequestRequeue**

**WdfRequestRetrieveInputBuffer**

**WdfRequestRetrieveInputMemory**

**WdfRequestRetrieveInputWdmMdl**

**WdfRequestRetrieveOutputBuffer**

**WdfRequestRetrieveOutputMemory**

**WdfRequestRetrieveOutputWdmMdl**

**WdfRequestRetrieveUnsafeUserInputBuffer**

**WdfRequestRetrieveUnsafeUserOutputBuffer**

**WdfRequestReuse**

**WdfRequestUnmarkCancelable**

**WdfSpinLockCreate**

**WdfStringCreate**

**WdfTimerCreate**

**WdfUsbInterfaceSelectSetting**

**WdfUsbTargetDeviceAllocAndQueryString**

**WdfUsbTargetDeviceCreate**

**WdfUsbTargetDeviceCyclePortSynchronously**

**WdfUsbTargetDeviceFormatRequestForControlTransfer**

**WdfUsbTargetDeviceFormatRequestForCyclePort**

**WdfUsbTargetDeviceFormatRequestForString**

**WdfUsbTargetDeviceFormatRequestForUrb**

**WdfUsbTargetDeviceIsConnectedSynchronous**

**WdfUsbTargetDeviceQueryString**

**WdfUsbTargetDeviceResetPortSynchronously**

**WdfUsbTargetDeviceRetrieveConfigDescriptor**

**WdfUsbTargetDeviceRetrieveCurrentFrameNumber**

**WdfUsbTargetDeviceRetrieveInformation**

**WdfUsbTargetDeviceSelectConfig**

**WdfUsbTargetDeviceSendControlTransferSynchronously**

**WdfUsbTargetDeviceSendUrbSynchronously**

**WdfUsbTargetPipeAbortSynchronously**

**WdfUsbTargetPipeConfigContinuousReader**

**WdfUsbTargetPipeFormatRequestForAbort**

**WdfUsbTargetPipeFormatRequestForRead**

**WdfUsbTargetPipeFormatRequestForReset**

**WdfUsbTargetPipeFormatRequestForUrb**

**WdfUsbTargetPipeFormatRequestForWrite**

**WdfUsbTargetPipeReadSynchronously**

**WdfUsbTargetPipeResetSynchronously**

**WdfUsbTargetPipeSendUrbSynchronously**

**WdfUsbTargetPipeWriteSynchronously**

**WdfWaitLockAcquire**

**WdfWaitLockCreate**

**WdfWmiInstanceCreate**

**WdfWmiInstanceFireEvent**

**WdfWmiInstanceRegister**

**WdfWmiProviderCreate**

**WdfWorkItemCreate**

 

 





