---
title: PowerIrpDDIs 规则（wdm）
description: PowerIrpDDIs 规则指定当驱动程序使用 IRP MN 设置的电源处理系统或设备 IRP \_ MJ \_ 功能时 \_ \_ \_ ，它不应调用只能在被动级别调用的 DDIs \_ 。
ms.assetid: C56C73E5-75D6-427A-8582-24D6B1404A70
ms.date: 05/21/2018
keywords:
- PowerIrpDDIs 规则（wdm）
topic_type:
- apiref
api_name:
- PowerIrpDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2bc9e5a92bd560c7fc730382b943e32011d69271
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918071"
---
# <a name="powerirpddis-rule-wdm"></a>PowerIrpDDIs 规则（wdm）


**PowerIrpDDIs**规则指定当驱动程序使用 irp MN 设置的电源处理系统或设备 IRP \_ MJ 功能时 \_ \_ \_ \_ ，它不应调用只能在被动级别调用的 DDIs \_ 。

**驱动程序模型： WDM**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>PowerIrpDDIs</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**ExIsProcessorFeaturePresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisprocessorfeaturepresent)  
[**ExRaiseAccessViolation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraiseaccessviolation)  
[**ExRaiseDatatypeMisalignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exraisedatatypemisalignment)  
[**ExUuidCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exuuidcreate)  
[**HalExamineMBR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-halexaminembr)  
[**HalGetInterruptVector**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))  
[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)  
[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)  
[**IoCheckShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocheckshareaccess)  
[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)  
[**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)  
[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)  
[**IoCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)  
[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)  
[**IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)  
[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)  
[**IoDeleteSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink)  
[**IoDetachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodetachdevice)  
[**IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)  
[**IoGetConfigurationInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetconfigurationinformation)  
[**IoGetDeviceInterfaceAlias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacealias)  
[**IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)  
[**IoGetDeviceNumaNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicenumanode)  
[**Plxntb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)  
[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)  
[**IoGetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicepropertydata)  
[**IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter)  
[**IoGetFileObjectGenericMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetfileobjectgenericmapping)  
[**IoInitializeTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)  
[**IoIsWdmVersionAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiswdmversionavailable)  
[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)  
[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)  
[**IoRegisterBootDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)  
[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)  
[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)  
[**IoRegisterLastChanceShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterlastchanceshutdownnotification)  
[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)  
[**IoRegisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregistershutdownnotification)  
[**IoRemoveShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioremoveshareaccess)  
[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)  
[**IoReportTargetDeviceChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreporttargetdevicechange)  
[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)  
[**IoSetDevicePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdevicepropertydata)  
[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)  
[**IoUnregisterPlugPlayNotificationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotificationex)  
[**IoUnregisterShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregistershutdownnotification)  
[**IoUpdateShareAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioupdateshareaccess)  
[**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiallocateinstanceids)  
[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)  
[**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)  
[**KeInitializeSemaphore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializesemaphore)  
[**KeQueryPriorityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryprioritythread)  
[**KeQueryRuntimeThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryruntimethread)  
[**KeRevertToUserAffinityThreadEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereverttouseraffinitythreadex)  
[**KeSetSystemAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetsystemaffinitythread)  
[**KeSetSystemGroupAffinityThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetsystemgroupaffinitythread)  
[**MmGetSystemRoutineAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemroutineaddress)  
[**PsGetVersion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psgetversion)  
[**PsRemoveLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-psremoveloadimagenotifyroutine)  
[**PsSetCreateProcessNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutine)  
[**PsSetCreateProcessNotifyRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreateprocessnotifyroutineex)  
[**PsSetCreateThreadNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetcreatethreadnotifyroutine)  
[**PsSetLoadImageNotifyRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pssetloadimagenotifyroutine)  
[**PsTerminateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-psterminatesystemthread)  
[**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)  
[**SeAssignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seassignsecurity)  
[**SeDeassignSecurity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-sedeassignsecurity)  
[**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)  
[**SeValidSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-sevalidsecuritydescriptor)  
[**ZwAllocateLocallyUniqueId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwallocatelocallyuniqueid)  
[**ZwAllocateVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566416)  
[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)  
[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)  
[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)  
[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)  
[**ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)  
[**ZwCreateKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekeytransacted)  
[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)  
[**ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)  
[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)  
[**ZwDeleteFile**](https://msdn.microsoft.com/library/windows/hardware/ff566435)  
[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)  
[**ZwDeleteValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletevaluekey)  
[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)  
[**ZwDuplicateToken**](https://msdn.microsoft.com/library/windows/hardware/ff566446)  
[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)  
[**ZwEnumerateTransactionObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntenumeratetransactionobject)  
[**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)  
[**ZwFlushBuffersFile**](https://msdn.microsoft.com/library/windows/hardware/ff566454)  
[**ZwFreeVirtualMemory**](https://msdn.microsoft.com/library/windows/hardware/ff566460)  
[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)  
[**ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)  
[**ZwLoadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwloaddriver)  
[**ZwLockFile**](https://msdn.microsoft.com/library/windows/hardware/ff566474)  
[**ZwMakeTemporaryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmaketemporaryobject)  
[**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)  
[**ZwNotifyChangeKey**](https://msdn.microsoft.com/library/windows/hardware/ff566488)  
[**ZwOpenDirectoryObject**](https://msdn.microsoft.com/library/windows/hardware/ff566492)  
[**ZwOpenEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenenlistment)  
[**ZwOpenEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenevent)  
[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)  
[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)  
[**ZwOpenKeyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeyex)  
[**ZwOpenKeyTransacted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeytransacted)  
[**ZwOpenKeyTransactedEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkeytransactedex)  
[**ZwOpenProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ntopenprocess)  
[**ZwOpenProcessTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567024)  
[**ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensection)  
[**ZwOpenSymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopensymboliclinkobject)  
[**ZwOpenThreadTokenEx**](https://msdn.microsoft.com/library/windows/hardware/ff567032)  
[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)  
[**ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)  
[**ZwPowerInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpowerinformation)  
[**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)  
[**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)  
[**ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)  
[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)  
[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)  
[**ZwQueryEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961907)  
[**ZwQueryFullAttributesFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryfullattributesfile)  
[**ZwQueryInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)  
[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)  
[**ZwQueryInformationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationresourcemanager)  
[**ZwQueryInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567055)  
[**ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)  
[**ZwQueryInformationTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)  
[**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)  
[**ZwQueryObject**](https://msdn.microsoft.com/library/windows/hardware/ff567062)  
[**ZwQueryQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567064)  
[**ZwQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567066)  
[**ZwQuerySymbolicLinkObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerysymboliclinkobject)  
[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)  
[**ZwQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567070)  
[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)  
[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)  
[**ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)  
[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)  
[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)  
[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)  
[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)  
[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)  
[**ZwSetEaFile**](https://msdn.microsoft.com/library/windows/hardware/ff961908)  
[**ZwSetInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment)  
[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)  
[**ZwSetInformationThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwsetinformationthread)  
[**ZwSetInformationToken**](https://msdn.microsoft.com/library/windows/hardware/ff567102)  
[**ZwSetInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationtransaction)  
[**ZwSetQuotaInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567105)  
[**ZwSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff567106)  
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)  
[**ZwSetVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567112)  
[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)  
[**ZwTerminateProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-zwterminateprocess)  
[**ZwUnloadDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunloaddriver)  
[**ZwUnlockFile**](https://msdn.microsoft.com/library/windows/hardware/ff567118)  
[**ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwunmapviewofsection)  
[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)  
 

 





