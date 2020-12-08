---
title: 带批注的 x86 反汇编
description: 带批注的 x86 反汇编
keywords:
- x86 处理器，带批注的反汇编
- x86 处理器，程序集代码
- x86 处理器，源代码
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8486df640d533c0e215e1c7c262fdfc86f8a98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819321"
---
# <a name="annotated-x86-disassembly"></a>带批注的 x86 反汇编


## <span id="ddk_annotated_x86_disassembly_dbg"></span><span id="DDK_ANNOTATED_X86_DISASSEMBLY_DBG"></span>


以下部分将指导你完成反汇编示例。

### <a name="span-idsource_codespanspan-idsource_codespanspan-idsource_codespansource-code"></a><span id="Source_Code"></span><span id="source_code"></span><span id="SOURCE_CODE"></span>源代码

下面是要分析的函数的代码。

```cpp
HRESULT CUserView::CloseView(void)
{
    if (m_fDestroyed) return S_OK;

    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);

    if (m_psv) {
        m_psb->EnableModelessSB(FALSE);
        if(m_pws) m_pws->ViewReleased();

        IShellView* psv;

        HWND hwndCapture = GetCapture();
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }

        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
        NotifyClients(m_psv, NOTIFY_CLOSING);
        m_fRecursing = FALSE;

        m_psv->UIActivate(SVUIA_DEACTIVATE);

        psv = m_psv;
        m_psv = NULL;

        ReleaseAndNull(&_pctView);

        if (m_pvo) {
            IAdviseSink *pSink;
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
                if (pSink == (IAdviseSink *)this)
                    m_pvo->SetAdvise(0, 0, NULL);
                pSink->Release();
            }

            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
        }

        if (psv) {
            psv->SaveViewState();
            psv->DestroyViewWindow();
            psv->Release();
        }

        m_hwndView = NULL;
        m_fHandsOff = FALSE;

        if (m_pcache) {
            GlobalFree(m_pcache);
            m_pcache = NULL;
        }

        m_psb->EnableModelessSB(TRUE);

        CancelPendingActions();
    }

    ReleaseAndNull(&_psf);

    if (fViewObjectChanged)
        NotifyViewClients(DVASPECT_CONTENT, -1);

    if (m_pszTitle) {
        LocalFree(m_pszTitle);
        m_pszTitle = NULL;
    }

    SetRect(&m_rcBounds, 0, 0, 0, 0);
    return S_OK;
}
```

### <a name="span-idassembly_codespanspan-idassembly_codespanspan-idassembly_codespanassembly-code"></a><span id="Assembly_Code"></span><span id="assembly_code"></span><span id="ASSEMBLY_CODE"></span>程序集代码

本部分包含带批注的反汇编示例。

使用 **ebp** 寄存器作为帧指针的函数如下所示：

```dbgcmd
HRESULT CUserView::CloseView(void)
SAMPLE!CUserView__CloseView:
71517134 55               push    ebp
71517135 8bec             mov     ebp,esp
```

这将设置框架，以便函数可以将其参数作为来自 **ebp** 的正偏移，并将局部变量作为负偏移量来访问。

这是私有 COM 接口上的方法，因此调用约定为 **\_ \_ stdcall**。 这意味着，在这种情况下，参数将向左推送 (在这种情况下，没有任何) ，推送 "this" 指针，然后调用函数。 因此，在进入函数后，堆栈如下所示：

```dbgcmd
[esp+0] = return address
[esp+4] = this
```

在上述两个说明之后，可以通过以下方式访问参数：

```dbgcmd
[ebp+0] = previous ebp pushed on stack
[ebp+4] = return address
[ebp+8] = this
```

对于使用 **ebp** 作为帧指针的函数，第一个推送的参数在 ebp + 8 上是可访问的 \[ **ebp** \] ; 后续参数可以在连续的更高 DWORD 地址上访问。

```dbgcmd
71517137 51               push    ecx
71517138 51               push    ecx
```

此函数只需要两个本地堆栈变量，因此，一个 **子 esp**，8个指令。 然后，可将推送的值用作 \[ **ebp**-4 \] 和 \[ **ebp**-8 \] 。

对于使用 **ebp** 作为帧指针的函数，可以从 **ebp** 寄存器的负偏移量访问 stack 局部变量。

```dbgcmd
71517139 56               push    esi
```

现在，编译器会保存需要跨函数调用保留的寄存器。 实际上，它将它们保存在位和部分，并与实际代码的第一行交叉。

```dbgcmd
7151713a 8b7508           mov     esi,[ebp+0x8]     ; esi = this
7151713d 57               push    edi               ; save another registers
```

因此，CloseView 是 ViewState 上的一种方法，该方法在基础对象的偏移量为12。 因此， **这** 是指向 ViewState 类的指针，不过，当可能与其他基类混淆时，将更仔细地将其指定为 (ViewState \*) **此** 类。

```dbgcmd
    if (m_fDestroyed)
7151713e 33ff             xor     edi,edi           ; edi = 0
```

XORing 的寄存器是其自身的一种标准方式。

```dbgcmd
71517140 39beac000000     cmp     [esi+0xac],edi    ; this->m_fDestroyed == 0?
71517146 7407             jz      NotDestroyed (7151714f)  ; jump if equal
```

**Cmp** 指令比较两个值 (通过将它们) 减去它们。 **Jz** 指令检查结果是否为零，表示两个比较的值相等。

Cmp 指令比较两个值;后续 j 指令根据比较结果跳转。

```dbgcmd
    return S_OK;
71517148 33c0             xor     eax,eax           ; eax = 0 = S_OK
7151714a e972010000       jmp     ReturnNoEBX (715172c1) ; return, do not pop EBX
```

编译器会将 EBX 注册延迟保存到函数的后面，因此，如果该程序要在此测试上 "提前"，则退出路径需要是不还原 EBX 的路径。

```dbgcmd
    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);
```

这两行代码是交错执行的，因此需要注意。

```dbgcmd
NotDestroyed:
7151714f 8d86c0000000     lea     eax,[esi+0xc0]    ; eax = &m_pdtgt
```

**逆转** 指令计算内存访问的效果地址，并将其存储在目标中。 不取消引用实际的内存地址。

逆转指令采用变量的地址。

```dbgcmd
71517155 53               push    ebx
```

应在 EBX 注册损坏之前保存。

```dbgcmd
71517156 8b1d10195071     mov ebx,[_imp__ReleaseAndNull]
```

由于你将频繁地调用 **ReleaseAndNull** ，因此最好在 EBX 中缓存其地址。

```dbgcmd
7151715c 50               push    eax               ; parameter to ReleaseAndNull
7151715d 897dfc           mov     [ebp-0x4],edi     ; fViewObjectChanged = FALSE
71517160 ffd3             call    ebx               ; call ReleaseAndNull
    if (m_psv) {
71517162 397e74           cmp     [esi+0x74],edi    ; this->m_psv == 0?
71517165 0f8411010000     je      No_Psv (7151727c) ; jump if zero
```

请记住，在回拨后已将 EDI 注册 a，并且该 EDI 是跨函数调用保留的寄存器 (因此对 **ReleaseAndNull** 的调用不会将其更改) 。 因此，它仍保留零值，你可以使用它来快速测试零。

```dbgcmd
        m_psb->EnableModelessSB(FALSE);
7151716b 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151716e 57               push    edi               ; FALSE
7151716f 50               push    eax               ; "this" for callee
71517170 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
71517172 ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
```

以上模式是 COM 方法调用的 telltale 符号。

COM 方法调用非常受欢迎，因此最好知道识别它们。 具体而言，你应该能够直接从其 Vtable 偏移量中识别三个 IUnknown 方法： QueryInterface = 0、AddRef = 4 和 Release = 8。

```dbgcmd
        if(m_pws) m_pws->ViewReleased();
71517175 8b8614010000     mov     eax,[esi+0x114]   ; eax = this->m_pws
7151717b 3bc7             cmp     eax,edi           ; eax == 0?
7151717d 7406             jz      NoWS (71517185) ; if so, then jump
7151717f 8b08             mov     ecx,[eax]         ; ecx = m_pws->lpVtbl
71517181 50               push    eax               ; "this" for callee
71517182 ff510c           call    [ecx+0xc]         ; __stdcall ViewReleased
NoWS:
        HWND hwndCapture = GetCapture();
71517185 ff15e01a5071    call [_imp__GetCapture]    ; call GetCapture
```

通过 globals 进行的间接调用是指在 Microsoft Win32 中如何实现函数导入。 加载器将修复全局，以指向目标的实际地址。 当调查崩溃的计算机时，可以使用此方法轻松获取 bearings。 查找对导入函数和目标中的的调用。 你通常会获得一些导入函数的名称，你可以使用该名称来确定你在源代码中所处的位置。

```dbgcmd
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }
7151718b 3bc7             cmp     eax,edi           ; hwndCapture == 0?
7151718d 7412             jz      No_Capture (715171a1) ; jump if zero
```

函数返回值放置在 EAX 寄存器中。

```dbgcmd
7151718f 8b4e44           mov     ecx,[esi+0x44]    ; ecx = this->m_hwnd
71517192 3bc1             cmp     eax,ecx           ; hwndCapture = ecx?
71517194 750b             jnz     No_Capture (715171a1) ; jump if not

71517196 57               push    edi               ; 0
71517197 57               push    edi               ; 0
71517198 6a1f             push    0x1f              ; WM_CANCELMODE
7151719a 51               push    ecx               ; hwndCapture
7151719b ff1518195071     call    [_imp__SendMessageW] ; SendMessage
No_Capture:
        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
715171a1 66818e0c0100000180 or    word ptr [esi+0x10c],0x8001 ; set both flags at once

        NotifyClients(m_psv, NOTIFY_CLOSING);
715171aa 8b4e20           mov     ecx,[esi+0x20]    ; ecx = (CNotifySource*)this.vtbl
715171ad 6a04             push    0x4               ; NOTIFY_CLOSING
715171af 8d4620           lea     eax,[esi+0x20]    ; eax = (CNotifySource*)this
715171b2 ff7674           push    [esi+0x74]        ; m_psv
715171b5 50               push    eax               ; "this" for callee
715171b6 ff510c           call    [ecx+0xc]         ; __stdcall NotifyClients
```

请注意，在您自己的其他基类上调用方法时，如何更改 "this" 指针。

```dbgcmd
        m_fRecursing = FALSE;
715171b9 80a60d0100007f   and     byte ptr [esi+0x10d],0x7f
        m_psv->UIActivate(SVUIA_DEACTIVATE);
715171c0 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171c3 57               push    edi               ; SVUIA_DEACTIVATE = 0
715171c4 50               push    eax               ; "this" for callee
715171c5 8b08             mov     ecx,[eax]         ; ecx = vtbl
715171c7 ff511c           call    [ecx+0x1c]        ; __stdcall UIActivate
        psv = m_psv;
        m_psv = NULL;
715171ca 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171cd 897e74           mov     [esi+0x74],edi    ; m_psv = NULL
715171d0 8945f8           mov     [ebp-0x8],eax     ; psv = eax
```

第一个本地变量为 **psv**。

```dbgcmd
        ReleaseAndNull(&_pctView);
715171d3 8d466c           lea     eax,[esi+0x6c]    ; eax = &_pctView
715171d6 50               push    eax               ; parameter
715171d7 ffd3             call    ebx               ; call ReleaseAndNull
        if (m_pvo) {
715171d9 8b86a8000000     mov     eax,[esi+0xa8]    ; eax = m_pvo
715171df 8dbea8000000     lea     edi,[esi+0xa8]    ; edi = &m_pvo
715171e5 85c0             test    eax,eax           ; eax == 0?
715171e7 7448             jz      No_Pvo (71517231) ; jump if zero
```

请注意，编译器推测性准备了 **m \_ pvo** 成员的地址，因为你将频繁地使用它。 这样，地址越方便，代码就越小。

```dbgcmd
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
715171e9 8b08             mov     ecx,[eax]         ; ecx = m_pvo->lpVtbl
715171eb 8d5508           lea     edx,[ebp+0x8]     ; edx = &pSink
715171ee 52               push    edx               ; parameter
715171ef 6a00             push    0x0               ; NULL
715171f1 6a00             push    0x0               ; NULL
715171f3 50               push    eax               ; "this" for callee
715171f4 ff5120           call    [ecx+0x20]        ; __stdcall GetAdvise
715171f7 85c0             test    eax,eax           ; test bits of eax
715171f9 7c2c             jl      No_Advise (71517227) ; jump if less than zero
715171fb 33c9             xor     ecx,ecx           ; ecx = 0
715171fd 394d08           cmp     [ebp+0x8],ecx     ; _pSink == ecx?
71517200 7425             jz      No_Advise (71517227)
```

请注意，编译器会发现传入的 "this" 参数 (不是必需的，因为它很久之前储藏更改到 ESI 注册) 。 因此，它重复使用内存作为本地变量 pSink。

如果该函数使用了 EBP 帧，则传入的参数将以正偏移量从 EBP 开始，并将局部变量置于负偏移位置。 但在这种情况下，编译器可以出于任何目的自由重用该内存。

如果你要密切关注，你会发现编译器可以更好地优化此代码。 它可能会延迟 **逆转 edi， \[ esi + 0xa8 \]** 指令直到两个 **push 0x0** 指令后，将它们替换为 **推送 edi**。 这会节省2个字节。

```dbgcmd
                if (pSink == (IAdviseSink *)this)
```

接下来的几行是为了弥补这一事实：在 c + + 中， (IAdviseSink \*) **NULL** 仍必须为 **null**。 因此，如果 "this" 确实 " (ViewState \*) null"，则强制转换的结果应为 **null** ，而不是 IAdviseSink 和 IBrowserService 之间的距离。

```dbgcmd
71517202 8d46ec           lea     eax,[esi-0x14]    ; eax = -(IAdviseSink*)this
71517205 8d5614           lea     edx,[esi+0x14]    ; edx = (IAdviseSink*)this
71517208 f7d8             neg     eax               ; eax = -eax (sets carry if != 0)
7151720a 1bc0             sbb     eax,eax           ; eax = eax - eax - carry
7151720c 23c2             and     eax,edx           ; eax = NULL or edx
```

尽管 Pentium 有一个条件移动指令，但基本 i386 体系结构没有，因此，编译器将使用特定的技术来模拟条件移动指令，而无需执行任何跳转。

条件计算的常规模式如下：

```dbgcmd
        neg     r
        sbb     r, r
        and     r, (val1 - val2)
        add     r, val2
```

如果 **r** 为非零， **neg r** 将设置携带标志，因为 **neg** 将通过从零中减去来对值求反。 如果减去非零值，则与零相减会生成一个借用 () 集。 它还会损坏 **r** 寄存器中的值，但这是可接受的，因为你将始终覆盖它。

接下来， **sbb r，r** 指令从自身中减去一个值，该值始终为零。 不过，它还会将 (借用) 位，因此，最终结果是将 **r** 设置为0或-1，具体取决于是否已清除或设置该操作。

因此，如果 **r** 的原始值为零，则 **sbb r** 将 **r** 设置为零; 如果原始值为非零，则为-1。

第三个指令执行掩码。 由于 **r** 寄存器为零或-1，因此 "this" 可保留 **r** 零或将 **r** 从-1 更改为 **(Val1-val1)**，在该 ANDing 中，-1 的任何值都将保留原始值。

因此，如果 r 的原始值为零，则 "and r， (val1-val1) " 的结果是将 r 设置为零; 如果 r 的原始值为非零，则设置为 " (val1-val2) "。

最后，将 **val2** 添加到 **r**，导致 **val2** 或 **(val1-val2) + val2 = val1**。

因此，这一系列的说明的最终结果是将 **r** 设置为 **val2** （如果它最初为零，则设置为 **val1** ）。 这是 **r = r？ val1： val2** 的程序集等效项。

在此特定示例中，可以看到 **val2 = 0** ， **Val1 = (IAdviseSink \*) 此**。  (请注意，编译器省略了最终 **添加 eax，0指令，** 因为它不起作用。 ) 

```dbgcmd
7151720e 394508           cmp     [ebp+0x8],eax ; pSink == (IAdviseSink*)this?
71517211 750b             jnz     No_SetAdvise (7151721e) ; jump if not equal
```

在本部分前面部分，将 EDI 设置为 **m \_ pvo** 成员的地址。 你现在将使用它。 你还可以提前将 ECX 注册归零。

```dbgcmd
                    m_pvo->SetAdvise(0, 0, NULL);
71517213 8b07             mov     eax,[edi]         ; eax = m_pvo
71517215 51               push    ecx               ; NULL
71517216 51               push    ecx               ; 0
71517217 51               push    ecx               ; 0
71517218 8b10             mov     edx,[eax]         ; edx = m_pvo->lpVtbl
7151721a 50               push    eax               ; "this" for callee
7151721b ff521c           call    [edx+0x1c]        ; __stdcall SetAdvise
No_SetAdvise:
                pSink->Release();
7151721e 8b4508           mov     eax,[ebp+0x8]     ; eax = pSink
71517221 50               push    eax               ; "this" for callee
71517222 8b08             mov     ecx,[eax]         ; ecx = pSink->lpVtbl
71517224 ff5108           call    [ecx+0x8]         ; __stdcall Release
No_Advise:
```

所有这些 COM 方法调用都应该非常熟悉。

接下来的两个语句的计算是交错的。 请不要忘记，EBX 包含 **ReleaseAndNull** 的地址。

```dbgcmd
            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
71517227 57               push    edi               ; &m_pvo
71517228 c745fc01000000   mov     dword ptr [ebp-0x4],0x1 ; fViewObjectChanged = TRUE
7151722f ffd3             call    ebx               ; call ReleaseAndNull
No_Pvo:
        if (psv) {
71517231 8b7df8           mov     edi,[ebp-0x8]     ; edi = psv
71517234 85ff             test    edi,edi           ; edi == 0?
71517236 7412             jz      No_Psv2 (7151724a) ; jump if zero
            psv->SaveViewState();
71517238 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
7151723a 57               push    edi               ; "this" for callee
7151723b ff5034           call    [eax+0x34]        ; __stdcall SaveViewState
```

下面是更多 COM 方法调用。

```dbgcmd
            psv->DestroyViewWindow();
7151723e 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517240 57               push    edi               ; "this" for callee
71517241 ff5028           call    [eax+0x28]        ; __stdcall DestroyViewWindow
            psv->Release();
71517244 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517246 57               push    edi               ; "this" for callee
71517247 ff5008           call    [eax+0x8]         ; __stdcall Release
No_Psv2:
        m_hwndView = NULL;
7151724a 83667c00         and     dword ptr [esi+0x7c],0x0 ; m_hwndView = 0
```

使用零的内存位置 ANDing 与将其设置为零相同，因为任何内容和零均为零。 编译器使用此窗体，因为虽然速度较慢，但它比等效的 **mov** 指令要短得多。  (此代码已针对大小进行优化，而不是加速。 ) 

```dbgcmd
        m_fHandsOff = FALSE;
7151724e 83a60c010000fe   and     dword ptr [esi+0x10c],0xfe
        if (m_pcache) {
71517255 8b4670           mov     eax,[esi+0x70]    ; eax = m_pcache
71517258 85c0             test    eax,eax           ; eax == 0?
7151725a 740b             jz      No_Cache (71517267) ; jump if zero
            GlobalFree(m_pcache);
7151725c 50               push    eax               ; m_pcache
7151725d ff15b4135071     call    [_imp__GlobalFree]    ; call GlobalFree
            m_pcache = NULL;
71517263 83667000         and     dword ptr [esi+0x70],0x0 ; m_pcache = 0
No_Cache:
        m_psb->EnableModelessSB(TRUE);
71517267 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151726a 6a01             push    0x1               ; TRUE
7151726c 50               push    eax               ; "this" for callee
7151726d 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
7151726f ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
        CancelPendingActions();
```

若要调用 **CancelPendingActions**，必须从 (ViewState 转变 \*) 此 (\*) 此。 另请注意， **CancelPendingActions** 使用 \_ \_ thiscall 调用约定而不是 \_ \_ stdcall。 根据 \_ \_ thiscall，"this" 指针传入 ECX 寄存器，而不是传递到堆栈上。

```dbgcmd
71517272 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
71517275 e832fbffff       call CUserView::CancelPendingActions (71516dac) ; __thiscall
    ReleaseAndNull(&_psf);
7151727a 33ff             xor     edi,edi           ; edi = 0 (for later)
No_Psv:
7151727c 8d4678           lea     eax,[esi+0x78]    ; eax = &_psf
7151727f 50               push    eax               ; parameter
71517280 ffd3             call    ebx               ; call ReleaseAndNull
    if (fViewObjectChanged)
71517282 397dfc           cmp     [ebp-0x4],edi     ; fViewObjectChanged == 0?
71517285 740d             jz      NoNotifyViewClients (71517294) ; jump if zero
       NotifyViewClients(DVASPECT_CONTENT, -1);
71517287 8b46ec           mov     eax,[esi-0x14]    ; eax = ((CUserView*)this)->lpVtbl
7151728a 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
7151728d 6aff             push    0xff              ; -1
7151728f 6a01             push    0x1               ; DVASPECT_CONTENT = 1
71517291 ff5024           call    [eax+0x24]        ; __thiscall NotifyViewClients
NoNotifyViewClients:
    if (m_pszTitle)
71517294 8b8680000000     mov     eax,[esi+0x80]    ; eax = m_pszTitle
7151729a 8d9e80000000     lea     ebx,[esi+0x80]    ; ebx = &m_pszTitle (for later)
715172a0 3bc7             cmp     eax,edi           ; eax == 0?
715172a2 7409             jz      No_Title (715172ad) ; jump if zero
        LocalFree(m_pszTitle);
715172a4 50               push    eax               ; m_pszTitle
715172a5 ff1538125071     call   [_imp__LocalFree]
        m_pszTitle = NULL;
```

请记住，EDI 仍为零，EBX 仍 &m \_ pszTitle，因为这些寄存器由函数调用保留。

```dbgcmd
715172ab 893b             mov     [ebx],edi         ; m_pszTitle = 0
No_Title:
    SetRect(&m_rcBounds, 0, 0, 0, 0);
715172ad 57               push    edi               ; 0
715172ae 57               push    edi               ; 0
715172af 57               push    edi               ; 0
715172b0 81c6fc000000     add     esi,0xfc          ; esi = &this->m_rcBounds
715172b6 57               push    edi               ; 0
715172b7 56               push    esi               ; &m_rcBounds
715172b8 ff15e41a5071     call   [_imp__SetRect]
```

请注意，你不需要 "这" 的值，因此编译器将使用 **add** 指令就地修改它，而不是使用另一个寄存器来保存该地址。 这实际上是由于采用了 Pentium u/v 流水线操作而导致的性能入选，因为 v 管道可以进行算术运算，而不是地址计算。

```dbgcmd
    return S_OK;
715172be 33c0             xor     eax,eax           ; eax = S_OK
```

最后，您将还原所需的寄存器、清理堆栈并返回到调用方，并删除传入参数。

```dbgcmd
715172c0 5b               pop     ebx               ; restore
ReturnNoEBX:
715172c1 5f               pop     edi               ; restore
715172c2 5e               pop     esi               ; restore
715172c3 c9               leave                     ; restores EBP and ESP simultaneously
715172c4 c20400           ret     0x4               ; return and clear parameters
```

 

 





