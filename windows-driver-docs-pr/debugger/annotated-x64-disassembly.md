---
title: 带批注的 x64 反汇编
description: 带批注的 x64 反汇编
keywords:
- x64 处理器，带批注的反汇编
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bf471c02485d6709aa5e2b1e1983966f5fea46
ms.sourcegitcommit: b17e8a4c9ed6503e844416b4ca3f8c38199c1b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2021
ms.locfileid: "103193331"
---
# <a name="annotated-x64-disassembly"></a>带批注的 x64 反汇编


## <span id="ddk_annotated_x64_disassembly_dbg"></span><span id="DDK_ANNOTATED_X64_DISASSEMBLY_DBG"></span>


下面非常简单的函数说明了 x64 调用约定。

```cpp
int Simple(int i, int j)
{
    return i*5 + j + 3;
}
```

这将编译为类似于下面的代码：

```dbgcmd
01001080 lea     eax,[rdx+rcx*4]        ; eax = rdx+rcx*4
01001083 lea     eax,[rcx+rax+0x3]      ; eax = rcx+rax+3
01001087 ret
```

*I* 和 *j* 参数分别在 **ecx** 和 **edx** 寄存器中传递。 由于只有两个参数，例程根本不使用堆栈。

生成的特定代码利用三个技巧，其中一种是特定于 x64 的：

1.  **逆转** 操作可用于将一系列简单的算术运算作为单个操作执行。 第一条指令在 eax 中存储 *j + i* \* 4，第二个指令将 *i*+ 3 添加到结果，总共 *j* + *i* \* 5 + 3。

2.  许多运算（如加法和乘法）可以通过额外的精度来完成，然后截断为正确的精度。 在此实例中，代码使用64位加法和乘法。 可以安全地将结果截断为32位。

3.  在 x64 上，任何输出到32位寄存器的操作都将自动零扩展结果。 在这种情况下，输出到 **eax** 的效果是将结果截断为32位。

返回值是在 **rax** 寄存器中传递的。 在这种情况下，结果已在 **rax** 注册中，因此该函数返回。

接下来，我们考虑使用更复杂的函数来演示典型的 x64 反汇编：

```cpp
HRESULT Meaningless(IDispatch *pdisp, DISPID dispid, BOOL fUnique, LPCWSTR pszExe)
{
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
    if (SUCCEEDED(hr)) {
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);
        if (SUCCEEDED(hr)) {
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {
                VARIANTARG rgvarg[2] = { 0 };
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {
                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }
        }
        pqa->Release();
    }
    return hr;
}
```

我们将通过行来完成此函数和等效的程序集。

输入时，函数的参数按如下方式存储：

-   **rcx**  = *pdisp*。

-   **rdx**  = *dispid*。

-   **r8**  = *fUnique*。

-   **r9**  = *pszExe*。

请记住，在寄存器中传递了前四个参数。 由于此函数只有四个寄存器，因此不会在堆栈上传递任何。

程序集的开头如下所示：

```dbgcmd
Meaningless:
010010e0 push    rbx                    ; save
010010e1 push    rsi                    ; save
010010e2 push    rdi                    ; save
010010e3 push    r12d                   ; save
010010e5 push    r13d                   ; save
010010e7 push    r14d                   ; save
010010e9 push    r15d                   ; save
010010eb sub     rsp,0x2c0              ; reserve stack
010010f2 mov     rbx,r9                 ; rbx = pszExe
010010f5 mov     r12d,r8d               ; r12 = fUnique (zero-extend)
010010f8 mov     r13d,edx               ; r13 = dispid  (zero-extend)
010010fb mov     rsi,rcx                ; rsi = pdisp
```

函数首先保存非易失寄存器，然后保留用于本地变量的堆栈空间。 然后，它将在非易失寄存器中保存参数。 请注意，中间两个 **mov** 指令的目标是32位寄存器，因此它们隐式扩展到64位。

```dbgcmd
    IQueryAssociations *pqa;
    HRESULT hr = AssocCreate(CLSID_QueryAssociations, IID_IQueryAssociations, (void**)&pqa);
```

**AssocCreate** 的第一个参数是通过值传递的128位 CLSID。 由于它不适合64位寄存器，因此会将 CLSID 复制到堆栈，并改为传递指向堆栈位置的指针。

```dbgcmd
010010fe movdqu  xmm0,oword ptr [CLSID_QueryAssociations (01001060)]
01001106 movdqu  oword ptr [rsp+0x60],xmm0  ; temp buffer for first parameter
0100110c lea     r8,[rsp+0x58]          ; arg3 = &pqa
01001111 lea rdx,[IID_IQueryAssociations (01001070)] ; arg2 = &IID_IQueryAssociations
01001118 lea     rcx,[rsp+0x60]         ; arg1 = &temporary
0100111d call qword ptr [_imp_AssocCreate (01001028)] ; call
```

**Movdqu** 指令将128位值与 **xmm**_n_ 寄存器之间传输。 在此实例中，程序集代码使用它将 CLSID 复制到堆栈。 指向 CLSID 的指针传递在 **r8** 中。 另外两个参数传递在 **rcx** 和 **rdx** 中。

```dbgcmd
    if (SUCCEEDED(hr)) {

01001123 test    eax,eax
01001125 jl      ReturnEAX (01001281)
```

代码将检查返回值是否成功。

```dbgcmd
        hr = pqa->Init(ASSOCF_INIT_BYEXENAME, pszExe, NULL, NULL);

0100112b mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001130 mov     rax,[rcx]              ; rax = pqa.vtbl
01001133 xor     r14d,r14d              ; r14 = 0
01001136 mov     [rsp+0x20],r14         ; arg5 = 0
0100113b xor     r9d,r9d                ; arg4 = 0
0100113e mov     r8,rbx                 ; arg3 = pszExe
01001141 mov     r15d,0x2               ; r15 = 2 (for later)
01001147 mov     edx,r15d               ; arg2 = 2 (ASSOCF_INIT_BY_EXENAME)
0100114a call    qword ptr [rax+0x18]   ; call Init method
```

这是使用 c + + vtable 的间接函数调用。 **This** 指针在 **rcx** 中作为第一个参数传递。 前三个参数在寄存器中传递，而最后一个参数传递到堆栈上。 此函数为寄存器中传递的参数保留16个字节，因此第五个参数从 **rsp**+ 0x20 开始。

```dbgcmd
        if (SUCCEEDED(hr)) {

0100114d mov     ebx,eax                ; ebx = hr
0100114f test    ebx,ebx                ; FAILED?
01001151 jl      ReleasePQA (01001274)  ; jump if so
```

汇编语言代码将结果保存在 **ebx** 中，并检查是否为成功代码。

```dbgcmd
            WCHAR wszName[MAX_PATH];
            DWORD cchName = MAX_PATH;
            hr = pqa->GetString(0, ASSOCSTR_FRIENDLYAPPNAME, NULL, wszName, &cchName);
            if (SUCCEEDED(hr)) {

01001157 mov     dword ptr [rsp+0x50],0x104 ; cchName = MAX_PATH
0100115f mov     rcx,[rsp+0x58]         ; arg1 = pqa
01001164 mov     rax,[rcx]              ; rax = pqa.vtbl
01001167 lea     rdx,[rsp+0x50]         ; rdx = &cchName
0100116c mov     [rsp+0x28],rdx         ; arg6 = cchName
01001171 lea     rdx,[rsp+0xb0]         ; rdx = &wszName[0]
01001179 mov     [rsp+0x20],rdx         ; arg5 = &wszName[0]
0100117e xor     r9d,r9d                ; arg4 = 0
01001181 mov     r8d,0x4                ; arg3 = 4 (ASSOCSTR_FRIENDLYNAME)
01001187 xor     edx,edx                ; arg2 = 0
01001189 call    qword ptr [rax+0x20]   ; call GetString method
0100118c mov     ebx,eax                ; ebx = hr
0100118e test    ebx,ebx                ; FAILED?
01001190 jl      ReleasePQA (01001274)  ; jump if so
```

接下来，我们设置参数并调用一个函数，然后测试返回值是否成功。

```dbgcmd
                VARIANTARG rgvarg[2] = { 0 };

01001196 lea     rdi,[rsp+0x82]         ; rdi = &rgvarg
0100119e xor     eax,eax                ; rax = 0
010011a0 mov     ecx,0x2e               ; rcx = sizeof(rgvarg)
010011a5 rep     stosb                  ; Zero it out
```

用于对 x64 上的缓冲区进行清零的惯用方法与 x86 相同。

```dbgcmd
                V_VT(&rgvarg[0]) = VT_BSTR;
                V_BSTR(&rgvarg[0]) = SysAllocString(wszName);
                if (V_BSTR(&rgvarg[0])) {

010011a7 mov     word ptr [rsp+0x80],0x8 ; V_VT(&rgvarg[0]) = VT_BSTR
010011b1 lea     rcx,[rsp+0xb0]         ; arg1 = &wszName[0]
010011b9 call    qword ptr [_imp_SysAllocString (01001010)] ; call
010011bf mov     [rsp+0x88],rax         ; V_BSTR(&rgvarg[0]) = result
010011c7 test    rax,rax                ; anything allocated?
010011ca je      OutOfMemory (0100126f) ; jump if failed

                    DISPPARAMS dp;
                    LONG lUnique = InterlockedIncrement(&lCounter);

010011d0 lea     rax,[lCounter (01002000)]
010011d7 mov     ecx,0x1
010011dc lock    xadd [rax],ecx             ; interlocked exchange and add
010011e0 add     ecx,0x1
```

**InterlockedIncrement** 直接编译到计算机代码。 **Lock xadd** 指令执行原子交换并添加。 最终的结果存储在 **ecx** 中。

```dbgcmd
                    V_VT(&rgvarg[1]) = VT_I4;
                    V_I4(&rgvarg[1]) = fUnique ? lUnique : 0;

010011e3 mov     word ptr [rsp+0x98],0x3    ; V_VT(&rgvarg[1]) = VT_I4;
010011ed mov     eax,r14d                   ; rax = 0 (r14d is still zero)
010011f0 test    r12d,r12d                  ; fUnique set?
010011f3 cmovne  eax,ecx                    ; if so, then set rax=lCounter
010011f6 mov     [rsp+0xa0],eax             ; V_I4(&rgvarg[1]) = ...
```

由于 x64 支持 **cmov** 指令，因此无需使用跳转即可编译 **？：** 构造。

```dbgcmd
                    dp.rgvarg = rgvarg;
                    dp.cArgs = 2;
                    dp.rgdispidNamedArgs = NULL;
                    dp.cNamedArgs = 0;

010011fd lea     rax,[rsp+0x80]             ; rax = &rgvarg[0]
01001205 mov     [rsp+0x60],rax             ; dp.rgvarg = rgvarg
0100120a mov     [rsp+0x70],r15d            ; dp.cArgs = 2 (r15 is still 2)
0100120f mov     [rsp+0x68],r14             ; dp.rgdispidNamedArgs = NULL
01001214 mov     [rsp+0x74],r14d            ; dp.cNamedArgs = 0
```

此代码初始化 DISPPARAMS 的其余成员。 请注意，编译器将重用以前由 CLSID 使用的堆栈上的空间。

```dbgcmd
                    hr = pdisp->Invoke(dispid, IID_NULL, 0, DISPATCH_METHOD, &dp, NULL, NULL, NULL);

01001219 mov     rax,[rsi]                  ; rax = pdisp.vtbl
0100121c mov     [rsp+0x40],r14             ; arg9 = 0
01001221 mov     [rsp+0x38],r14             ; arg8 = 0
01001226 mov     [rsp+0x30],r14             ; arg7 = 0
0100122b lea     rcx,[rsp+0x60]             ; rcx = &dp
01001230 mov     [rsp+0x28],rcx             ; arg6 = &dp
01001235 mov     word ptr [rsp+0x20],0x1    ; arg5 = 1 (DISPATCH_METHOD)
0100123c xor     r9d,r9d                    ; arg4 = 0
0100123f lea     r8,[GUID_NULL (01001080)]  ; arg3 = &IID_NULL
01001246 mov     edx,r13d                   ; arg2 = dispid
01001249 mov     rcx,rsi                    ; arg1 = pdisp
0100124c call    qword ptr [rax+0x30]       ; call Invoke method
0100124f mov     ebx,eax                    ; hr = result
```

然后，该代码设置参数并调用 **Invoke** 方法。

```dbgcmd
                    VariantClear(&rgvarg[0]);
                    VariantClear(&rgvarg[1]);

01001251 lea     rcx,[rsp+0x80]             ; arg1 = &rgvarg[0]
01001259 call    qword ptr [_imp_VariantClear (01001018)]
0100125f lea     rcx,[rsp+0x98]             ; arg1 = &rgvarg[1]
01001267 call    qword ptr [_imp_VariantClear (01001018)]
0100126d jmp     ReleasePQA (01001274)
```

代码完成条件的当前分支，并跳过 **else** 分支。

```dbgcmd
                } else {
                    hr = E_OUTOFMEMORY;
                }
            }

OutOfMemory:
0100126f mov     ebx,0x8007000e             ; hr = E_OUTOFMEMORY
        pqa->Release();
ReleasePQA:
01001274 mov     rcx,[rsp+0x58]             ; arg1 = pqa
01001279 mov     rax,[rcx]                  ; rax = pqa.vtbl
0100127c call    qword ptr [rax+0x10]       ; release
```

**Else** 分支。

```dbgcmd
    return hr;
}

0100127f mov     eax,ebx                    ; rax = hr (for return value)
ReturnEAX:
01001281 add     rsp,0x2c0                  ; clean up the stack
01001288 pop     r15d                       ; restore
0100128a pop     r14d                       ; restore
0100128c pop     r13d                       ; restore
0100128e pop     r12d                       ; restore
01001290 pop     rdi                        ; restore
01001291 pop     rsi                        ; restore
01001292 pop     rbx                        ; restore
01001293 ret                                ; return (do not pop arguments)
```

返回值存储在 **rax** 中，然后在返回前还原非易失性寄存器。

## <a name="see-also"></a>另请参阅

[x64 体系结构](x64-architecture.md)

[X86-64 维基百科](https://en.wikipedia.org/wiki/X86-64)

 





