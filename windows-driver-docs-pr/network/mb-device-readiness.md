---
title: MB 设备就绪状态
description: MB 设备就绪状态
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: de2847f127adaba1f838ccd414a079d2210e8a6c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247815"
---
# <a name="mb-device-readiness"></a>MB 设备就绪状态


本主题介绍了在 MB 服务继续设置数据连接之前确保 MB 设备可用于网络相关活动的步骤。 当用户订阅已激活并且存储到设备或订阅服务器标识模块 (SIM 卡时，设备可供使用) 

MB 服务假定微型端口驱动程序在系统加载它后，自动初始化其 MB 设备的硬件 (无线电堆栈、SIM 卡或等效电路) ，而无需等待来自服务的任何指令。

微型端口驱动程序将其 MB 设备的初始就绪状态设置为 **WwanReadyStateOff**。 当他们继续初始化时，微型端口驱动程序必须发送事件通知，以通知 MB 服务对其设备就绪状态的更改。

如果小型端口驱动程序遇到任何错误条件，则必须停止该初始化过程。 清除错误条件后，微型端口驱动程序可以恢复初始化过程，直到其设备达到 **WwanReadyStateInitialized** 就绪状态。

下面是一些错误情况的示例：

-   如果设备要求使用 SIM 卡，而微型端口驱动程序检测到不存在 SIM 卡，则微型端口驱动程序必须发送 **WwanReadyStateSimNotInserted** 就绪状态事件通知，并且在用户将 SIM 卡插入设备之前，微型端口驱动程序必须保持该状态。

-   如果设备要求使用 SIM 卡，而微型端口驱动程序无法读取已插入的 SIM 卡 (例如，将 U 形插入到基于 GSM 的设备中，或将 USIM 插入到基于 CDMA 的设备中) 或 SIM 卡与设备不兼容 (例如，3G USIM 插入到2G 设备中，这种设备无法解释 USIM 格式) ，微型端口驱动程序必须发送 **WwanReadyStateBadSim** ready 状态事件通知，而微型端口驱动程序必须保持该状态，直到用户将正确的 SIM 卡插入到设备中。

-   如果设备被 PIN (锁定，使用 SIM 卡) 或通过密码 (对于不使用 SIM 卡) 阻止进一步设备初始化进度的设备，微型端口驱动程序必须发送 **WwanReadyStateDeviceLocked** 的就绪状态事件通知，并且在用户输入正确的 PIN 或密码之前，微型端口驱动程序必须保持该状态。

-   如果微型端口驱动程序检测到需要进行服务激活，则微型端口驱动程序必须发送 **WwanReadyStateNotActivated** 就绪状态事件通知，并且必须保持该状态，直到服务已激活。 这是北美中基于 CDMA 的设备的典型行为。

-   如果微型端口驱动程序运行的不是前面提到的故障，微型端口驱动程序必须发送 **WwanReadyStateFailure** 就绪状态事件通知，并且必须保持该状态，直到已识别并更正问题。

请注意，MB 服务不假定微型端口驱动程序可以检测所有这些错误。 服务也不会假设小型小型驱动程序检测这些错误情况的顺序。 不过，最好按照前面列出的顺序来实现错误方案。

在微型端口驱动程序发送 **WwanReadyStateInitialized** 的就绪状态事件通知之前，该服务将不会继续进行与网络相关的活动，直到发现并更正该问题。 但是，该服务仍可以将 Oid 发送到微型端口驱动程序。

在报告 **WwanReadyStateInitialized** 就绪状态之前，微型端口驱动程序无需等待 SMS 子系统准备就绪。 相反，小型端口驱动程序应在 SMS 子系统准备发送和接收短信时发送单独的 [OID \_ WWAN \_ SMS \_ 配置](./oid-wwan-sms-configuration.md) 通知。

### <a name="emergency-mode-support"></a>紧急模式支持

如果微型端口驱动程序指示它支持在处理 [OID \_ WWAN \_ 可用 \_ 信息](./oid-wwan-ready-info.md)时进行紧急呼叫服务，微型端口驱动程序必须将 " [**WWAN \_ 就绪 \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ready_info)结构" 的 **EmergencyMode** 成员设置为 " **WwanEmergencyModeOn**"。 在这种情况下，微型端口驱动程序应继续将注册通知发送到 MB 服务，但该服务不会调用任何自动配置相关的功能。

微型端口驱动程序可以指定它们支持紧急呼叫服务，即使在检测到 SIM 失效的情况下也是如此，原因可能是订阅未付款，或服务已被停用，因为设备已被报告为被盗。

## <a name="mb-miniport-driver-initialization"></a>MB 微型端口驱动程序初始化

下图显示了确定接口是否为限定的 MB 接口以及收集有关设备功能的信息所采取的过程。 当启动 MB 服务时，将为每个枚举的 MB 接口执行这些步骤，并在服务运行时针对每个新的接口到达执行这些步骤。 以粗体显示的标签表示 OID 标识符或事务流控制。 常规文本中的标签表示 OID 结构中的重要标志。

![如果接口是限定的 mb 接口并收集有关设备功能的信息，则建立](images/wwandriverinitproc.png)

若要初始化 MB 微型端口驱动程序，请使用以下过程：

1.  MB 服务发送同步 (阻塞) OID 生成 [ \_ \_ 物理 \_ 中型](oid-gen-physical-medium.md) 查询请求来识别 MB 设备的类型。 微型端口驱动程序通过 **NdisPhysicalMediumWirelessWan** 进行响应，以指示 MB 设备为 WWAN 设备。

2.  MB 服务向微型端口驱动程序发送同步 (阻止) [OID 生成 \_ \_ 媒体 \_ 支持](oid-gen-media-supported.md) 的查询请求，以确定 MB 设备使用的介质类型。 微型端口驱动程序使用 **NdisMedium802 \_ 3** 进行响应，以指示它使用以太网模拟。

3.  MB 服务向微型端口驱动程序发送同步 (阻止) [OID \_ WWAN \_ 驱动程序 \_ cap](oid-wwan-driver-caps.md) 查询请求，以确定微型端口驱动程序支持的驱动程序型号版本。 微型端口驱动程序以 WWAN \_ 版本响应。

4.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 设备 \_ cap](oid-wwan-device-caps.md) 查询请求，以确定 MB 设备的功能。 微型端口驱动程序使用其收到请求的临时确认进行响应，并且它将在将来发送包含所需信息的通知。

5.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 设备 \_ Cap**](ndis-status-wwan-device-caps.md) 通知发送到 mb 服务，该服务指示微型端口驱动程序支持的 mb 设备的功能。 例如，如果微型端口驱动程序支持基于 GSM 的设备，则它应在 [**NDIS \_ WWAN \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构的 **DeviceCaps. WwanCellularClass** 成员中指定 **WwanCellularClassGsm** 值。 如果微型端口驱动程序支持基于 CDMA 的设备，则应指定 **WwanCellularClassCdma**。

## <a name="initialization-of-sim-locked-gprs-device-with-a-user-defined-context"></a>使用 User-Defined 上下文初始化 SIM-Locked GPRS 设备


下图演示了用户输入 SIM PIN 并手动配置访问点名称字符串的情况。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明用户输入 sim pin 并手动配置访问点名称字符串的方案的关系图](images/wwanlockedgsmdevinitseq.png)

若要初始化 PIN1 锁定的基于 GSM 的设备，请执行以下步骤：

1.  MB 服务向微型端口驱动程序发送异步 (非阻塞) [OID \_ WWAN \_ 就绪 \_ 信息](oid-wwan-ready-info.md) 查询请求，以标识设备的就绪状态。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

2.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 失败通知发送到 mb 服务，以向 mb 服务指明订阅服务器标识模块 (SIM) 锁定。

3.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 固定](oid-wwan-pin.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

4.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

5.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 固定](oid-wwan-pin.md) 请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

6.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

7.  微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 就绪 \_ 信息**](ndis-status-wwan-ready-info.md) 通知发送到 mb 服务，该服务向 mb 服务指示 Mb 设备的状态为 " **WwanReadyStateInitialized**"。

8.  MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 注册 \_ 状态](oid-wwan-register-state.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

9.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

10. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](ndis-status-wwan-register-state.md) 通知发送到 MB 服务。

11. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ \_ 提供程序](oid-wwan-home-provider.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

12. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 成功通知发送到 MB 服务。

13. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 注册 \_ 状态**](ndis-status-wwan-register-state.md) 通知发送到 MB 服务。

14. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 数据包 \_ 服务](oid-wwan-packet-service.md) 请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

15. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 数据包 \_ 服务**](ndis-status-wwan-packet-service.md) 通知发送到 MB 服务。

16. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](oid-wwan-provisioned-contexts.md) 查询请求发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

17. 微型端口驱动程序将 [**NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文**](ndis-status-wwan-provisioned-contexts.md) 发送到 MB 服务。

18. MB 服务将异步 (非阻塞) [OID \_ WWAN \_ 预配 \_ 上下文](oid-wwan-provisioned-contexts.md) 集请求发送到 MB 服务。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

19. 微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

## <a name="see-also"></a>另请参阅

有关设备准备情况的详细信息，请参阅 [OID \_ WWAN \_ 就绪 \_ 信息](oid-wwan-ready-info.md)。

有关具有预配上下文的设备初始化的详细信息，请参阅 [MB 预配的上下文操作](mb-provisioned-context-operations.md)。

 

