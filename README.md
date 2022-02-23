# CaixaAltaBaixa
FunçãoSqlCaixaBaixaAlta


 FUNCTION CaixaAltaBaixa (@StrValue AS VARCHAR(150))
RETURNS VARCHAR(150)
AS
  BEGIN
      DECLARE @AUX AS VARCHAR(151)
      DECLARE @TEMP AS VARCHAR(100)
      DECLARE @TEMP2 AS VARCHAR(100)
      DECLARE @RESULT AS VARCHAR(100)
      DECLARE @Y AS INT

      SET @Y = 0
      SET @AUX = Rtrim(Ltrim(@StrValue)) + ' '
      SET @RESULT = ''

      WHILE @Y < 1
        BEGIN
            SET @TEMP = Substring(@AUX, 1, Charindex(' ', @AUX))
            SET @AUX = Substring(@AUX, Charindex(' ', @AUX) + 1, Len(@AUX))
            SET @TEMP2 = Upper(Substring(@TEMP, 1, 1)) + Lower(Substring(@TEMP, 2, Len(@TEMP)))

            IF Charindex(CHAR(39), @TEMP2) <> 0
              BEGIN
                  SET @TEMP2 = Substring(@TEMP2, 1, Charindex(CHAR(39), @TEMP2)) 
        + Upper(Substring(Substring(@TEMP2, Charindex(CHAR(39), @TEMP2) + 1, Len(@TEMP2)), 1, 1)) 
        + Lower(Substring(Substring(@TEMP2, Charindex(CHAR(39), @TEMP2) + 1, Len(@TEMP2)), 2, Len(@TEMP)))
              END

            IF Isnull(Charindex(' ', @AUX), 0) = 0
              BEGIN
                  SET @Y = 2
              END

            SET @RESULT = @RESULT + @TEMP2
        END

      SET @RESULT = REPLACE(@RESULT, ' E ', ' e ')
      SET @RESULT = REPLACE(@RESULT, ' DE ', ' de ')
      SET @RESULT = REPLACE(@RESULT, ' DA ', ' da ')
      SET @RESULT = REPLACE(@RESULT, ' DO ', ' do ')
      SET @RESULT = REPLACE(@RESULT, ' DAS ', ' das ')
      SET @RESULT = REPLACE(@RESULT, ' DOS ', ' dos ')

      RETURN @RESULT
  END
