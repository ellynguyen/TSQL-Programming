# TSQL-Programming
##XML PARSE
select *
FROM dbo.Template AS t	
OUTER APPLY (SELECT  tnm.value('./@LanguageId','int') AS TemplateNameLanguaID
          ,tnm.value('./@DisplayName','varchar(100)') TemplateName
      FROM t.NameXML.nodes('/root/TemplateName') AS tn(tnm)
      WHERE tnm.value('./@LanguageId','int') IN (@LanguageID,@DefLanguageID)
      ) AS tnm
