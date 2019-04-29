---
title: 建立临时网络连接
description: 建立临时网络连接
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff0a3a43aec6a585a67c4a44a74ce05d7ce734c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380170"
---
# <a name="establish-temporary-network-connectivity"></a>建立临时网络连接


电信服务应用程序不能启动长期的连接。 但是，如果您需要为特定网络的临时连接，可以使用移动宽带 API，如下所示：

1.  创建的实例[ **IMbnConnectionManager**](https://msdn.microsoft.com/library/windows/desktop/dd430380)。

2.  注册到[ **IMbnConnectionEvents** ](https://msdn.microsoft.com/library/windows/desktop/dd430375)连接点。

3.  创建的实例[ **IMbnInterfaceManager**](https://msdn.microsoft.com/library/windows/desktop/dd430416)。

4.  获取[ **IMbnInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430406)通过将传递到的帐户的设备 ID 的设备接口[ **IMbnInterfaceManager::GetInterface** ](https://msdn.microsoft.com/library/windows/desktop/dd430420). (有关详细信息，请参阅[解锁设备](unlock-a-device.md)。)

5.  通过调用获取设备的 IMbnConnection 接口[ **IMbnConnectionManager::GetConnection**](https://msdn.microsoft.com/library/windows/desktop/dd430384)。

6.  通过调用建立[ **IMbnConnection::Connect**](https://msdn.microsoft.com/library/windows/desktop/dd430399)。 *ConnectionMode*参数必须设置为**MBN\_连接\_模式\_TMP\_配置文件**，和*strProfile*参数必须是移动宽带的配置文件说明。

使用返回的连接尝试结果[ **IMbnConnectionEvents::OnConnectComplete** ](https://msdn.microsoft.com/library/windows/desktop/dd430376)方法。 若要断开连接完成后，请调用[ **IMbnConnection::Disconnect** ](https://msdn.microsoft.com/library/windows/desktop/dd430401)方法。 通过使用返回状态[ **IMbnConnectionEvents::OnDisconnectComplete**](https://msdn.microsoft.com/library/windows/desktop/dd430378)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






