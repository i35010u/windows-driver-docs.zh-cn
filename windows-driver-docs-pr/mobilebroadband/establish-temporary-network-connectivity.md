---
title: 建立临时网络连接
description: 建立临时网络连接
ms.assetid: 5ee9d1ab-cc6f-4262-b2b0-e8b0b0c0c1d3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d2d37126c25185b20435bc3ef9e9085f228dba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381470"
---
# <a name="establish-temporary-network-connectivity"></a>建立临时网络连接


电信服务应用程序不能启动长期的连接。 但是，如果您需要为特定网络的临时连接，可以使用移动宽带 API，如下所示：

1.  创建的实例[ **IMbnConnectionManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionmanager)。

2.  注册到[ **IMbnConnectionEvents** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbnconnectionevents)连接点。

3.  创建的实例[ **IMbnInterfaceManager**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterfacemanager)。

4.  获取[ **IMbnInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nn-mbnapi-imbninterface)通过将传递到的帐户的设备 ID 的设备接口[ **IMbnInterfaceManager::GetInterface** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface). (有关详细信息，请参阅[解锁设备](unlock-a-device.md)。)

5.  通过调用获取设备的 IMbnConnection 接口[ **IMbnConnectionManager::GetConnection**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionmanager-getconnection)。

6.  通过调用建立[ **IMbnConnection::Connect**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-connect)。 *ConnectionMode*参数必须设置为**MBN\_连接\_模式\_TMP\_配置文件**，和*strProfile*参数必须是移动宽带的配置文件说明。

使用返回的连接尝试结果[ **IMbnConnectionEvents::OnConnectComplete** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-onconnectcomplete)方法。 若要断开连接完成后，请调用[ **IMbnConnection::Disconnect** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnection-disconnect)方法。 通过使用返回状态[ **IMbnConnectionEvents::OnDisconnectComplete**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionevents-ondisconnectcomplete)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 Api 的常见任务](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






