---
title: fightclub
displaytext: Fight Club
layout:  col-sidebar
tab: true
order: 2
tags: sydney
---

### Fight Club leaderboard

See our running leaderboard below!

<html>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://unpkg.com/purecss@2.0.5/build/pure-min.css" integrity="sha384-LTIDeidl25h2dPxrB2Ekgc9c7sEC3CWGM6HeFmuDNUjX76Ert4Z4IY714dhZHPLd" crossorigin="anonymous">

    <script type="text/javascript">
      // Client ID and API key from the Developer Console
      var API_KEY = 'AIzaSyDb7ok3LcF6KueDIZD-dYrNxNOJ42ZAaME';
      var DISCOVERY_DOCS = ["https://sheets.googleapis.com/$discovery/rest?version=v4"];
      var SCOPES = "https://www.googleapis.com/auth/spreadsheets.readonly";
      var SHEETID = '1OdNhicU2fIi8jyRek5Ny0rhGhMaqXSTj2H3fTENO-yg';

      function handleClientLoad() {
        gapi.load('client', initClient);
      }

      function initClient() {
        gapi.client.init({
          apiKey: API_KEY,
          discoveryDocs: DISCOVERY_DOCS
        }).then(function(){listleaderboard();})
      }

      function createTable(table, data, numRows, numCols) {
        table.style.width = '40%';
        table.setAttribute('class', 'pure-table pure-table-horizontal');

        var th = table.insertRow();
        var header = data[0];

        for (j = 0; j < numCols; j++) {
          th.style.backgroundColor = '#BCBCBC';
          th.style.fontWeight = 'bold';
          var td = th.insertCell();
          td.appendChild(document.createTextNode(header[j]));
        }

        for (i = 1; i < numRows; i++) {
          var tr = table.insertRow();
          var row = data[i];

          if (i%2 != 0) {
              tr.setAttribute('class', 'pure-table-odd');
          }

          for (j = 0; j < numCols; j++) {
              var td = tr.insertCell();
              td.appendChild(document.createTextNode(row[j]));
          }
        }

        document.getElementById("sec-fightclub").appendChild(table);
      }

      function listleaderboard() {
        gapi.client.sheets.spreadsheets.values.get({
          spreadsheetId: SHEETID,
          range: 'A1:C',
        }).then(function(response) {
          var range = response.result;
          var data = range.values;
          var numRows = range.values.length;
          var numCols = 3;
          var table = document.createElement('table');

          createTable(table, data, numRows, numCols);

        }, function(response) {
          var err = document.createTextNode('Error: Please screnshot this message and contact the OWASP Chapter Leaders to report this');
          document.getElementById("sec-fightclub").appendChild(err);
        });
      }
    </script>

    <script async defer src="https://apis.google.com/js/api.js"
      onload="this.onload=function(){};handleClientLoad()"
      onreadystatechange="if (this.readyState === lete') this.onload()">
    </script>
</html>
