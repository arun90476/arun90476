SELECT 
    IBGPO.DINum,
    IBGPO.PONum AS IBGPO_PONum,         -- Not funded PO from IBGPO
    PaidIBGPO.PONum AS PaidIBGPO_PONum, -- Funded PO from PaidIBGPO
    IBGDI.DINum AS IBGDI_DINum          -- DINum from IBGDI (which is essentially a reference)
FROM 
    IBGPO
LEFT JOIN 
    PaidIBGPO ON IBGPO.DINum = PaidIBGPO.DINum  -- LEFT JOIN to include all IBGPO records, even if there's no matching record in PaidIBGPO
JOIN 
    IBGDI ON IBGPO.DINum = IBGDI.DINum          -- JOIN with IBGDI to match DINum
WHERE 
    IBGPO.DINum = ?;  -- Replace '?' with the specific DINum you are searching for
