---
title: Método ICorDebugNativeFrame::GetLocalDoubleRegisterValue
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalDoubleRegisterValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalDoubleRegisterValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalDoubleRegisterValue method [.NET Framework debugging]
- GetLocalDoubleRegisterValue method [.NET Framework debugging]
ms.assetid: 1f838215-ac8a-434f-8ce6-03021d3098d9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed7436ff73fa9cc19790859581930875f39e499e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746291"
---
# <a name="icordebugnativeframegetlocaldoubleregistervalue-method"></a>Método ICorDebugNativeFrame::GetLocalDoubleRegisterValue
Obtém o valor de um argumento ou uma variável local que é armazenado nos dois registradores especificados para este quadro nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalDoubleRegisterValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CorDebugRegister   lowWordReg,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `highWordReg`  
 [in] Um valor de enumeração "CorDebugRegister" que especifica o registro que contém a palavra alta do valor.  
  
 `lowWordReg`  
 [in] Um valor da `CorDebugRegister` enumeração que especifica o registro que contém a palavra inferior do valor.  
  
 `cbSigBlob`  
 [in] Um inteiro que especifica o tamanho da assinatura de metadados binária que é referenciado pelo `pvSigBlob` parâmetro.  
  
 `pvSigBlob`  
 [in] Um `PCCOR_SIGNATURE` valor que aponta para a assinatura binária metadados de tipo de valor.  
  
 `ppValue`  
 [out] Um ponteiro para o endereço de um objeto de "ICorDebugValue" que representa o valor recuperado armazenado nos registradores especificados.  
  
## <a name="remarks"></a>Comentários  
 O `GetLocalDoubleRegisterValue` método pode ser usado em um quadro nativo ou um just-in-time (JIT)-compilados do quadro.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também
