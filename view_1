CREATE VIEW portfolio_event_summary AS
SELECT 
    ev.event_id AS EventID,
    ev.procedure_date AS ProcedureDate,
    ev.hospital_name AS HospitalName,
    ev.status AS EventStatus,
    proc.procedure_name AS ProcedureName,
    proc.procedure_value AS ProcedureValue,
    proc.proportion AS ProcedureProportion,
    surg.surgeon_name AS SurgeonName,
    COUNT(DISTINCT ev.event_id) OVER(PARTITION BY surg.surgeon_id) AS TotalEventsBySurgeon,
    SUM(proc.procedure_value) OVER(PARTITION BY ev.hospital_name) AS TotalHospitalRevenue
FROM 
    event_table ev
JOIN 
    procedure_table proc ON ev.event_id = proc.event_id
JOIN 
    surgeon_table surg ON proc.surgeon_id = surg.surgeon_id
WHERE 
    ev.procedure_date BETWEEN '2023-01-01' AND '2023-12-31'
    AND ev.status = 'Completed';
