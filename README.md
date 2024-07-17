Handle Large Data

function copyLargeDataInBatches() {
  var sourceSpreadsheetId = 'SOURCE_SPREADSHEET_ID'; // Replace with your source spreadsheet ID
  var destinationSpreadsheetId = 'DESTINATION_SPREADSHEET_ID'; // Replace with your destination spreadsheet ID
  
  var sourceSpreadsheet = SpreadsheetApp.openById(sourceSpreadsheetId);
  var destinationSpreadsheet = SpreadsheetApp.openById(destinationSpreadsheetId);
  
  var sourceSheet = sourceSpreadsheet.getSheetByName('SourceSheetName'); // Replace with your source sheet name
  var destinationSheet = destinationSpreadsheet.getSheetByName('DestinationSheetName'); // Replace with your destination sheet name

  var range = sourceSheet.getDataRange();
  var values = range.getValues();

  var batchSize = 500; // Adjust the batch size as needed
  var startRow = 1;
  var endRow;

  destinationSheet.clear();

  while (startRow <= values.length) {
    endRow = Math.min(startRow + batchSize - 1, values.length);
    var batchValues = values.slice(startRow - 1, endRow);
    destinationSheet.getRange(startRow, 1, batchValues.length, batchValues[0].length).setValues(batchValues);
    startRow += batchSize;
  }

  Logger.log('Data copied successfully in batches');
}


