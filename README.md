SELECT 
    IBGPO.DINum,
    IBGPO.PONum AS PONum,
    'Not Funded' AS POStatus   -- Indicate that the PO is not funded
FROM 
    IBGPO
JOIN 
    IBGDI ON IBGPO.DINum = IBGDI.DINum  -- Make sure the DINum exists in IBGDI
WHERE 
    IBGPO.DINum = ?   -- Replace '?' with the specific DINum you're searching for

UNION ALL

SELECT 
    PaidIBGPO.DINum,
    PaidIBGPO.PONum AS PONum,
    'Funded' AS POStatus   -- Indicate that the PO is funded
FROM 
    PaidIBGPO
JOIN 
    IBGDI ON PaidIBGPO.DINum = IBGDI.DINum  -- Make sure the DINum exists in IBGDI
WHERE 
    PaidIBGPO.DINum = ?  -- Replace '?' with the specific DINum you're searching for
