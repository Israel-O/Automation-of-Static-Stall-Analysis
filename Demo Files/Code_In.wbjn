Save(Overwrite=True)
unitSystem1 = SetProjectUnitSystem(UnitSystemName="DesignModelerUnitSystem_m")
workDir = r"C:\Users\ogunm\OneDrive\Documents"
fileName = "\Input_Data.xlsx"
fileName2 = "\Results.csv"
logFile = open(AbsUserPathName(workDir+"\progress_logfile_report.log"), "w")

logFile.write("""+++++++++++++++++++++++++++++++++
+ANSYS Automated Stall Analysis++
+++++++++Israel Ogunmola+++++++++ 
+++++++++++++++++++++++++++++++++\n\n\n""")

ExcelInputColumns = ["A", "B", "C", "D"]
WorkbenchInputParam = ["P1","P2", "P3", "P6"]

import clr
clr.AddReference("Microsoft.Office.Interop.Excel")
import Microsoft.Office.Interop.Excel as Excel

ex = Excel.ApplicationClass()
ex.Visible = True
wb = ex.Workbooks.Open(workDir + fileName)
wsInput = wb.ActiveSheet
#wsOutput = wb.Worksheets.Add()
wsStatus = wb.Worksheets.Add()

#wsOutput.Name = "Output"
wsStatus.Name = "Status"
wsInput.Name = "Input"

def rowLength(col, chk): #col is a column "A", chk is true or false to include header or not
  row = 0
  val = wsInput.range[col + "1"].Value2
  logFile.write("    Checking length of row\n\n")
  while ((val == 0) | (val != None)):
    row = row+1
    val = wsInput.range[col + (row+1).ToString()].Value2
  if (chk == True): #If the first row is for Table Name, number of elements only
    logFile.write("Row length (elements only) : " + (row-1).ToString() + "\n")
    return abs(row - 1)
  logFile.write("Row length including header : " + row.ToString()+ "\n")
  return row

def dpCreator(rowLength): #Create x amount of design points
  counter = 1
  logFile.write("     Creating " + rowLength.ToString() + " Design Points\n\n")
  while counter < rowLength:
    Parameters.CreateDesignPoint(Name=counter.ToString())
    counter = counter + 1
  logFile.write("Design point success\n")

def deleteDp(start, stop): #Delete design points from start to stop
  counter = start
  logFile.write("   Deleting design points from " + start.ToString() + " to " + stop.ToString() + "\n")
  while counter <= stop:
    dp = Parameters.GetDesignPoint(Name=counter.ToString())
    dp.Delete()
    counter = counter + 1

  logFile.write("   Delete Success\n")

def assignParameterToDp(ExcelInputColumns, WorkbenchInputParam, ExcelDpColumn = "A"): #First and Second arguments are lists
  logFile.write("   Importing parameter from Excel\n")
  for i in range(rowLength("A", True)):
    dp = Parameters.GetDesignPoint(Name= (i).ToString())
    dp.Retained = False
    logFile.write("DesignPoint Data Retained \n\n")
    logFile.write("\t\t\tDesignPoint: " + (i).ToString() + "\n")
    for j in range(len(WorkbenchInputParam)):
      param = Parameters.GetParameter(Name=WorkbenchInputParam[j])
      dp.SetParameterExpression(Parameter=param, Expression=wsInput.Range[ExcelInputColumns[j]+(i+2).ToString()].Value2.ToString())
      logFile.write("Imported Parameter: " + param.ToString() + "\n")

def xlsResultFile(filePath, fileName2): #Make this the independent (I/O File) So you make this one first and the rest add to it
  Parameters.ExportAllDesignPointsData(FilePath=GetAbsoluteUserPathName(filePath+fileName2))
  logFile.write("\t\tReport Exported to Work Directory")

dpCreator(rowLength("A", True))
Save(Overwrite=True)
logFile.write("\t\t\tProject Saved")

assignParameterToDp(ExcelInputColumns, WorkbenchInputParam)
Save(Overwrite=True)
logFile.write("\t\t\tProject Saved")


try:
  UpdateAllDesignPoints()
  wsStatus.Range["A1"].Value2 = "Calculating"
  logFile.write("    Calculating...\n")
except:
  logFile.write("    Update failed.\n")
  wsStatus.Range["A1"].Value2 = "Failed"
else:
  logFile.write("    update succeeded\n")
  wsStatus.Range["A1"].Value2 = "Success!"

Save(Overwrite=True)
logFile.write("\t\t\tProject Saved")

reportLocation = workDir + "\EntireProjectReport.html"
ExportReport(FilePath=reportLocation)
logFile.write("      Report Exported\n")
xlsResultFile(workDir, fileName2)
logFile.write("      Results.csv Exported\n")
logFile.write("\t\t\tGoodbye")
logFile.close()

print("\n\nGoodBye")