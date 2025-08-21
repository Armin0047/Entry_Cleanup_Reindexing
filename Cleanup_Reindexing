-- Declare variables for tracking سند range and iteration
DECLARE @minsanad INT, @maxsanad INT, @nosanad INT;

-- Determine the minimum and maximum سند numbers for سال 1404
SELECT @minsanad = MIN(No_Sanad) FROM Hsb_De_Sanad WHERE Sal = 1404 AND No_Sanad IS NOT NULL;
SELECT @maxsanad = MAX(No_Sanad) FROM Hsb_De_Sanad WHERE Sal = 1404 AND No_Sanad IS NOT NULL;

-- Proceed only if valid range is found
IF (@minsanad > 0 AND @maxsanad > @minsanad)
BEGIN
    SET @nosanad = @minsanad;

    WHILE (@nosanad <= @maxsanad)
    BEGIN
        -- Check if سند exists in Hsb_Bod_Sanad
        IF EXISTS (SELECT 1 FROM Hsb_Bod_Sanad WHERE Sal = 1404 AND No_Sanad = @nosanad)
        BEGIN
            -- If سند does NOT exist in Hsb_De_Sanad, it's considered orphaned
            IF NOT EXISTS (SELECT 1 FROM Hsb_De_Sanad WHERE Sal = 1404 AND No_Sanad = @nosanad)
            BEGIN
                -- Delete orphaned سند from Hsb_Bod_Sanad
                DELETE FROM Hsb_Bod_Sanad WHERE Sal = 1404 AND No_Sanad = @nosanad;

                -- Reindex سند numbers in both tables to maintain continuity
                UPDATE Hsb_Bod_Sanad
                SET No_Sanad = No_Sanad - 1
                WHERE Sal = 1404 AND No_Sanad > @nosanad AND No_Sanad IS NOT NULL;

                UPDATE Hsb_De_Sanad
                SET No_Sanad = No_Sanad - 1
                WHERE Sal = 1404 AND No_Sanad > @nosanad AND No_Sanad IS NOT NULL;

                -- Do NOT increment @nosanad to recheck the new سند at this position
            END
            ELSE
            BEGIN
                -- سند is valid, move to next
                SET @nosanad = @nosanad + 1;
            END
        END
        ELSE
        BEGIN
            -- سند not found in Hsb_Bod_Sanad, skip to next
            SET @nosanad = @nosanad + 1;
        END
    END
END
