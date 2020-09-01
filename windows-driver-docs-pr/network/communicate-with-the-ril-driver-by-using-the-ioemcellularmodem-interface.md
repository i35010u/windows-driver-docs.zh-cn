---
title: 使用 IOemCellularModem 接口与 RIL 驱动程序通信
description: 本主题提供有关如何使用 IOemCellularModem 接口与 RIL 驱动程序通信的信息。
ms.assetid: 612a7f98-053f-4447-bb0e-c6f34969df5d
keywords:
- 使用 IOemCellularModem 接口网络驱动程序与 RIL 驱动程序通信
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ac6759437a8ca58d4d08e36194a60e964e6043
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208719"
---
# <a name="communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface"></a>使用 IOemCellularModem 接口与 RIL 驱动程序通信

> [!WARNING]
> Windows 10 中已弃用蜂窝 COM API。 提供此内容是为了支持维护 Windows Phone 8.1 应用程序创建的 OEM 和移动运营商。

可使用 [IOemCellularModem](/previous-versions/windows/hardware/cellular/dn946687(v=vs.85)) 接口与 OEM RIL 驱动程序通信。 在这种情况下，合作伙伴可以使用受限平台允许列表中的 Api (RPAL) 来与调制解调器通信。

有关蜂窝 COM Api 的详细信息，请参阅 [蜂窝 COM api 参考](/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))。

## <a name="using-cellular-com-apis"></a>使用蜂窝 COM Api

若要使用蜂窝 COM Api，请通过调用**CoCreateInstanceFromApp**获取指向[IOemCellular](/previous-versions/windows/hardware/cellular/dn946677(v=vs.85))实例的指针。 调用应用程序需要指向 IOemCellular 接口的指针，才能使用 [IOemCellularModem](/previous-versions/windows/hardware/cellular/dn946687(v=vs.85)) 接口。 

可以使用 [IOemCellular：： RegisterForOemModemExistenceChanges](/previous-versions/windows/hardware/cellular/dn931023(v=vs.85)) 方法列出调制解调器。 调用方法后，将调用 [IOemCellularModemExistenceChange：： OnOemModemAdded](/previous-versions/windows/hardware/cellular/dn946689(v=vs.85)) 和 [IOemCellularModem](/previous-versions/windows/hardware/cellular/dn946687(v=vs.85)) 指针。

此代码演示如何使用**CoCreateInstanceFromApp**检索[IOemCellular](/previous-versions/windows/hardware/cellular/dn946677(v=vs.85))指针。 CoCreateInstanceFromApp 可以返回一个或多个指向特定接口的指针。 所需的接口为 IOemCellular，由 query [0]. pIID 指定。 OemCellular 是对支持的 COM 类的引用;它确定激活类的工厂。 

```c++
    MULTI_QI query[1];
    query[0].pIID = &__uuidof(IOemCellular);
    query[0].pItf = nullptr;
    query[0].hr = S_OK;

    hr = CoCreateInstanceFromApp(__uuidof(OemCellular), nullptr, CLSCTX_INPROC_SERVER,
                                nullptr, _countof(query), query);
    ...
```
此代码演示如何使用[IOemCellular：： RegisterForOemModemExistenceChanges](/previous-versions/windows/hardware/cellular/dn931023(v=vs.85))注册指向[IOemCellularModemExistenceChange](/previous-versions/windows/hardware/cellular/dn946688(v=vs.85))的指针。 在下面的代码中，这是一个指向 **CModems** 的指针，它提供了 IOemCellularModemExistenceChange 接口。

```c++
    HRESULT hr;
    hr = m_spCellular->RegisterForOemModemExistenceChanges(this);

    ...
```

此代码演示如何实现 **OnOemModemAdded** 和 [IOemCellularModemExistenceChange](/previous-versions/windows/hardware/cellular/dn946688(v=vs.85)) 接口的其他方法。

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

## <a name="sending-opaque-data-to-ril"></a>将不透明数据发送到 RIL

通过调用**OnOemModemAdded**接收到**IOemCellularModem**指针后，可以使用[IOemCellularModem：： SendModemOpaqueCommand](/previous-versions/windows/hardware/cellular/dn931017(v=vs.85)) 。 在幕后，cellcore 调用 **RIL_DevSpecific** 函数和传递的参数。 RIL 驱动程序处理此请求，并将响应发送回上层。 在传递响应后，将使用**SendModemOpaqueCommand**调用的结果调用[IModemOpaqueCommandCompletion：： OnModemOpaqueCommandCompletion](/previous-versions/windows/hardware/cellular/dn946648(v=vs.85))的回调。

此代码显示了如何通过 [IOemCellularModem：： SendModemOpaqueCommand](/previous-versions/windows/hardware/cellular/dn931017(v=vs.85))发送不透明数据。

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

在上面的代码示例中，将向 RIL 发送一个命令，以便打开或关闭该无线电。 RIL 驱动程序应该设计为在调用 **RIL_DevSpecific** 时处理两个 DWORD 数据元素。 你可以定义自己的结构和命令以满足你的需求。 命令完成后，RIL 驱动程序将发送响应，然后调用 [IModemOpaqueCommandCompletion：： OnModemOpaqueCommandCompletion](/previous-versions/windows/hardware/cellular/dn946648(v=vs.85))) 的完成 (回调。 

此代码演示如何处理上一示例中的 **SendModemOpaqueCommand** 命令的接收完成事件。

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
> **最大请求、响应和通知大小** -RIL 适配层对 RIL 命令、响应和通知负载施加了 0x2800 (10240) 字节的最大大小约束。 负载越大，此大小就会生成错误。

## <a name="receiving-a-notification-from-ril"></a>接收来自 RIL 的通知

蜂窝接口提供了许多 RIL 通知，它们以 **RIL_NOTIFY**开头，如 **RIL_NOTIFY_SIGNALQUALITY**。 但 **IOemCellularModem** 不提供接收这些 RIL 通知的默认方法。 一种选择是将 [IOemCellularModem：： RegisterForOpaqueModemNotifications](/previous-versions/windows/hardware/cellular/dn931015(v=vs.85)) 用于这些 OEM RIL 通知。 为此，请首先定义你自己的 RIL 通知消息，该消息小于在 RilAPITypes 中定义的 **RIL_NOTIFY_OEM_MAX**。 只要 RIL 发送 OEM RIL 通知，就会在 IOemCellularModem：： RegisterForOpaqueModemNotifications 注册回调指针后调用 [IOpaqueModemNotifications：： OnOpaqueModemNotifications](/previous-versions/windows/hardware/cellular/dn931072(v=vs.85)) 。 

此代码演示如何调用 [IOemCellularModem：： RegisterForOpaqueModemNotifications](/previous-versions/windows/hardware/cellular/dn931015(v=vs.85))。

```c++
HRESULT CCellcoreComponent::CAgent::Initialize()
{
    ...
    IFFAILED_EXIT(m_spModem->RegisterForOpaqueModemNotifications(this));
    ...
```

此代码演示如何实现 [IOpaqueModemNotifications：： OnOpaqueModemNotifications](/previous-versions/windows/hardware/cellular/dn931072(v=vs.85))。 该代码包含一个通知回调句柄，该句柄返回信号条的数量。 应在调用应用程序和 RIL 驱动程序中实现自定义的通知 RIL_NOTIFY_OEM_SIGNALSTRENGTH。

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

[手机网络 COM API 设计指南](cellular-com-api-design-guide.md)

[蜂窝 COM API 参考](/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))