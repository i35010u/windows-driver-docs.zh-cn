---
title: 使用 IOemCellularModem 接口与 RIL 驱动程序进行通信
description: 本主题提供有关如何使用 IOemCellularModem 接口与 RIL 驱动程序进行通信的信息。
ms.assetid: 612a7f98-053f-4447-bb0e-c6f34969df5d
keywords:
- 使用 IOemCellularModem 接口网络驱动程序，使用 RIL 驱动程序进行通信
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29764ad9d165259d265ed55b7361b97cbf81aa99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369204"
---
# <a name="communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface"></a>使用 IOemCellularModem 接口与 RIL 驱动程序进行通信

> [!WARNING]
> 移动电话的 COM API 在 Windows 10 中已弃用。 提供此内容是为了支持 OEM 和移动运营商创建的 Windows Phone 8.1 应用程序的维护。

可以使用[IOemCellularModem](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946687(v=vs.85))接口与 OEM RIL 驱动程序进行通信。 这是一种情况合作伙伴可以使用受限制的平台中的 Api 允许列表 (RPAL) 与调制解调器进行通信。

有关移动电话的 COM Api 的详细信息，请参阅[移动电话的 COM API 参考](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))。

## <a name="using-cellular-com-apis"></a>使用移动电话的 COM Api

若要使用移动电话的 COM Api，获取一个指向[IOemCellular](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946677(v=vs.85))实例通过调用**CoCreateInstanceFromApp**。 调用应用程序所需使用此指向 IOemCellular 接口[IOemCellularModem](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946687(v=vs.85))接口。 

[IOemCellular::RegisterForOemModemExistenceChanges](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931023(v=vs.85))方法可用于列出调制解调器。 调用该方法后， [IOemCellularModemExistenceChange::OnOemModemAdded](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946689(v=vs.85))调用使用了[IOemCellularModem](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946687(v=vs.85))指针。

此代码演示如何检索[IOemCellular](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946677(v=vs.85))通过使用指针**CoCreateInstanceFromApp**。 CoCreateInstanceFromApp 可以返回到特定的接口的一个或多个指针。 所需的接口是 IOemCellular，指定的查询 [0].pIID。 OemCellular 是对支持的 COM 类; 的引用它确定激活类的工厂。 

```c++
    MULTI_QI query[1];
    query[0].pIID = &__uuidof(IOemCellular);
    query[0].pItf = nullptr;
    query[0].hr = S_OK;

    hr = CoCreateInstanceFromApp(__uuidof(OemCellular), nullptr, CLSCTX_INPROC_SERVER,
                                nullptr, _countof(query), query);
    ...
```
此代码显示了注册一个指向[IOemCellularModemExistenceChange](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946688(v=vs.85))通过使用[IOemCellular::RegisterForOemModemExistenceChanges](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931023(v=vs.85))。 在下面的代码，这是一个指向**CModems**它提供 IOemCellularModemExistenceChange 界面。

```c++
    HRESULT hr;
    hr = m_spCellular->RegisterForOemModemExistenceChanges(this);

    ...
```

此代码演示如何实现**OnOemModemAdded**和其他方法[IOemCellularModemExistenceChange](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946688(v=vs.85))接口。

```c++
class CModems : public IOemCellularModemExistenceChange, public CellBase
{
    ...

    // 
    // IOemCellularModemExistenceChange interface
    //
    IFACEMETHOD(OnOemModemAdded)(IOemCellularModem *pModem);
    IFACEMETHOD(OnOemModemRemoved)(IOemCellularModem *pModem);
    IFACEMETHOD(OnOemModemExistenceDone)();

    ...
};
IFACEMETHODIMP CModems::OnOemModemAdded(IOemCellularModem *pModem)
{
    ComPtr<IOemCellularModem> spModem(pModem);
    m_ModemList.push_back(spModem);
    return S_OK;
}
```

## <a name="sending-opaque-data-to-ril"></a>将不透明的数据发送到 RIL

在收到后**IOemCellularModem**指针通过调用**OnOemModemAdded**， [IOemCellularModem::SendModemOpaqueCommand](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931017(v=vs.85))可用。 在后台，移动电话核心调用**RIL_DevSpecific**函数使用传递的参数。 RIL 驱动程序处理此请求并发送响应返回给上层。 响应传递，对回调后[IModemOpaqueCommandCompletion::OnModemOpaqueCommandCompletion](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946648(v=vs.85))调用的结果与**SendModemOpaqueCommand**调用。

此代码显示了将使用的不透明数据发送[IOemCellularModem::SendModemOpaqueCommand](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931017(v=vs.85))。

```c++
    void CCellcoreComponent::CAgent::SetRadioPowerState(bool fPowerOn)
    {
        DWORD command[2];
        command[0] = CMD_SET_EQUIPMENTSTATE;
        command[1] = fPowerOn ? RIL_EQSTATE_FULL : RIL_EQSTATE_MINIMUM;
        m_spModem->SendModemOpaqueCommand(this, (BYTE*)command, sizeof(command), 
            (INT_PTR) CMD_SET_EQUIPMENTSTATE);
    ...
```

在上一代码示例中，若要启用或禁用单选命令发送到 RIL。 RIL 驱动程序应设计为处理的两个 DWORD 数据元素时**RIL_DevSpecific**调用。 可以定义自己的结构和命令以满足你的需求。 在命令完成之后, RIL 驱动程序将发送响应，然后完成回调 ([IModemOpaqueCommandCompletion::OnModemOpaqueCommandCompletion](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946648(v=vs.85))) 调用。 

此代码显示了处理的接收完成事件**SendModemOpaqueCommand**命令在前面的示例。

```c++
IFACEMETHODIMP CCellcoreComponent::CAgent::OnModemOpaqueCommandCompletion (
            /* [in] */ HRESULT result,
            /* [size_is][in] */ BYTE *pOpaqueResponse,
            /* [in] */ DWORD cbSize,
            /* [in] */ INT_PTR context)
{
    if (SUCCEEDED(result))
    {
        if ((int)context == CMD_SET_EQUIPMENTSTATE)
        {
            //
            // add routine if it is necessary to handle completion.
            //
        }
    }

    return S_OK;
}
```

> [!NOTE]
> **最大请求、 响应和通知大小**-RIL 适配层施加 RIL 命令、 响应和通知有效负载的 0x2800 (10240) 字节的最大大小约束。 负载较大，则此大小，将生成一个错误。

## <a name="receiving-a-notification-from-ril"></a>从 RIL 接收通知

移动电话网络接口提供了多个以开头的 RIL 通知**RIL_NOTIFY**，如**RIL_NOTIFY_SIGNALQUALITY**。 但是**IOemCellularModem**不会提供一个默认方法来接收这些 RIL 通知。 一种选择是使用[IOemCellularModem::RegisterForOpaqueModemNotifications](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931015(v=vs.85))这些 OEM RIL 通知。 若要执行此操作，首先定义是您自己 RIL 通知消息小于**RIL_NOTIFY_OEM_MAX**，RilAPITypes.h 中定义。 RIL 发送 OEM RIL 通知时，每当[IOpaqueModemNotifications::OnOpaqueModemNotifications](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931072(v=vs.85))后由 IOemCellularModem::RegisterForOpaqueModemNotifications 注册回调指针调用。 

此代码演示如何调用[IOemCellularModem::RegisterForOpaqueModemNotifications](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931015(v=vs.85))。

```c++
HRESULT CCellcoreComponent::CAgent::Initialize()
{
    ...
    IFFAILED_EXIT(m_spModem->RegisterForOpaqueModemNotifications(this));
    ...
```

此代码演示如何实现[IOpaqueModemNotifications::OnOpaqueModemNotifications](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn931072(v=vs.85))。 该代码包含返回的信号条数的通知回调句柄。 应实现自定义通知 RIL_NOTIFY_OEM_SIGNALSTRENGTH，在这两个调用应用程序和 RIL 驱动程序。

```c++
class CAgent : 
        public IOpaqueModemNotifications, 
        public IModemOpaqueCommandCompletion,
        public IPowerStateChange,
        public IPositionInfoCompletion,
        public IAgent
{
    ...

    //
    // IOpaqueModemNotifications
    //
    IFACEMETHOD(OnOpaqueModemNotifications)( 
    /* [in] */ DWORD dwCode,
    /* [in] */ BYTE *pOpaqueNotification,
    /* [in] */ DWORD cbSize);

                }
IFACEMETHODIMP CCellcoreComponent::CAgent::OnOpaqueModemNotifications( 
            /* [in] */ DWORD dwCode,
            /* [in] */ BYTE *pOpaqueNotification,
            /* [in] */ DWORD cbSize)
{
    wchar_t szResultString[STRING_BUF_LEN] = {0,};

    // check dwCode to fill notification result string.
    if (dwCode == RIL_NOTIFY_OEM_SIGNALSTRENGTH)
    {
        DWORD dwSignalBar;
        if (cbSize == sizeof(DWORD))
        {
            dwSignalBar = *((DWORD*)pOpaqueNotification);
        }
        else
        {
            dwSignalBar = -1;
        }

        swprintf_s(szResultString, STRING_BUF_LEN, L"Num of signal bars : %d", dwSignalBar );
    }
    else
    {
        swprintf_s(szResultString, STRING_BUF_LEN, L"Unknown Notification");
    }

    // send notification string.
    String ^ opaqueInfo = ref new String (szResultString);
    m_cellcore->OnOpaqueNotification(opaqueInfo);

    return S_OK;
}
```

## <a name="related-topics"></a>相关主题

[移动电话的 COM API 设计指南](cellular-com-api-design-guide.md)

[移动电话的 COM API 参考](https://docs.microsoft.com/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))

