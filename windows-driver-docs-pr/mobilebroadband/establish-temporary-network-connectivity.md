---
title: 建立临时网络连接
description: 建立临时网络连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9baf7ca6a88774a4389fa7b9b29cb29a182c0c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782343"
---
# <a name="establish-temporary-network-connectivity"></a>建立临时网络连接


电信应用程序无法启动长期连接。 但是，如果需要与特定网络进行临时连接，可以使用移动宽带 API，如下所示：

1.  创建 [**IMbnConnectionManager**](/windows/win32/api/mbnapi/nn-mbnapi-imbnconnectionmanager)的实例。

2.  注册到 [**IMbnConnectionEvents**](/windows/win32/api/mbnapi/nn-mbnapi-imbnconnectionevents) 连接点。

3.  创建 [**IMbnInterfaceManager**](/windows/win32/api/mbnapi/nn-mbnapi-imbninterfacemanager)的实例。

4.  通过将帐户设备 ID 传递到 [**IMbnInterfaceManager：： GetInterface**](/windows/win32/api/mbnapi/nf-mbnapi-imbninterfacemanager-getinterface)获取设备的 [**IMbnInterface**](/windows/win32/api/mbnapi/nn-mbnapi-imbninterface)接口。  (有关详细信息，请参阅 [解锁设备](unlock-a-device.md)。 ) 

5.  通过调用 [**IMbnConnectionManager：： GetConnection**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionmanager-getconnection)获取设备的 IMbnConnection 接口。

6.  通过调用 [**IMbnConnection：： Connect**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnection-connect)建立连接。 *ConnectionMode* 参数必须设置为 **MBN \_ 连接 \_ 模式 \_ TMP \_ 配置文件**，并且 *strProfile* 参数必须是移动宽带配置文件说明。

使用 [**IMbnConnectionEvents：： OnConnectComplete**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionevents-onconnectcomplete) 方法返回连接尝试的结果。 若要在完成后断开连接，请调用 [**IMbnConnection：:D isconnect**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnection-disconnect) 方法。 使用 [**IMbnConnectionEvents：： OnDisconnectComplete**](/windows/win32/api/mbnapi/nf-mbnapi-imbnconnectionevents-ondisconnectcomplete)返回状态。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[移动宽带 Windows 运行时 API 的常见任务](./create-a-mobilebroadbandaccount-object.md)

 

