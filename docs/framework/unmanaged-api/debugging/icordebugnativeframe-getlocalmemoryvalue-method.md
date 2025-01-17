---
title: Método ICorDebugNativeFrame::GetLocalMemoryValue
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalMemoryValue
helpviewer_keywords:
- GetLocalMemoryValue method [.NET Framework debugging]
- ICorDebugNativeFrame::GetLocalMemoryValue method [.NET Framework debugging]
ms.assetid: b600b3a2-9908-42d8-8093-ab6f39e9a2c9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9a8e5a1813a81a84eac612a53964d39b48f0c536
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746225"
---
# <a name="icordebugnativeframegetlocalmemoryvalue-method"></a>Método ICorDebugNativeFrame::GetLocalMemoryValue
Obtém o valor de um argumento ou uma variável local que é armazenado no local de memória especificado para este quadro nativo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetLocalMemoryValue (  
    [in]  CORDB_ADDRESS      address,  
    [in]  ULONG              cbSigBlob,  
    [in]  PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `address`  
 [in] Um `CORDB_ADDRESS` valor que especifica o local da memória que contém o valor.  
  
 `cbSigBlob`  
 [in] Um inteiro que especifica o tamanho da assinatura de metadados binária que é referenciado pelo `pvSigBlob` parâmetro.  
  
 `pvSigBlob`  
 [in] Um `PCCOR_SIGNATURE` valor que aponta para a assinatura binária metadados de tipo de valor.  
  
 `ppValue`  
 [out] Um ponteiro para o endereço de um objeto de "ICorDebugValue" que representa o valor recuperado armazenado no local da memória especificado.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** Confira [Requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também
