

<!DOCTYPE html>
<html lang="en" >

<head>

  <meta charset="UTF-8">
  
<link rel="apple-touch-icon" type="image/png" href="https://cpwebassets.codepen.io/assets/favicon/apple-touch-icon-5ae1a0698dcc2402e9712f7d01ed509a57814f994c660df9f7a952f3060705ee.png" />
<meta name="apple-mobile-web-app-title" content="CodePen">

<link rel="shortcut icon" type="image/x-icon" href="https://cpwebassets.codepen.io/assets/favicon/favicon-aec34940fbc1a6e787974dcd360f2c6b63348d4b1f4e06c77743096d55480f33.ico" />

<link rel="mask-icon" type="image/x-icon" href="https://cpwebassets.codepen.io/assets/favicon/logo-pin-8f3771b1072e3c38bd662872f6b673a722f4b3ca2421637d5596661b4e2132cc.svg" color="#111" />


  <title>CodePen - Trading Game_v2</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  
  <link rel='stylesheet' href='https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css'>
  
<style>
button, button:hover, button:active, button:focus, button:visited, .btn, .btn:hover, .btn:active, .btn:focus, .btn:visited {
  text-decoration: none !important;
  outline: none !important;
}

/* chart-section-container */
#chart-section-container {
  position: relative;
  height: 70%;
  min-height: 335px;
  width: 95%;
  margin: 5px auto;  
}
#loader-section {
  padding: 40px 0 30px 0;
}
.chart-buttons-container {
  position: absolute;
  background-color: transparent;
  display: none;
  top: 0;
  z-index: 1;
}
.chart-buttons-container button {
  border-radius: 0;
  font-size: 14px;
}
#chart-buttons-container-left { 
  left: 0;  
}
#chart-buttons-container-right { 
  right: 0;  
}
#data-speed-input {
  position: absolute;
  background-color: transparent;
  width: 120px;
  height: 20px;
  top: 4px;
  right: 60px;
  --min: 1;
  --max: 20;  
  --px: 1px;
  --range: calc(var(--max) - var(--min));
  --ratio: calc((var(--val) - var(--min))/var(--range));
  --sx: calc((var(--ratio)*120+10)*var(--px));  
}
#data-speed-input:focus { outline: none; }
#data-speed-input, #data-speed-input::-webkit-slider-thumb { -webkit-appearance: none; }
#data-speed-input::-webkit-slider-runnable-track {
  box-sizing: border-box;
  border: none;
  width: 120px;
  height: 5px;
  background: #ccc;
}
#data-speed-input::-webkit-slider-runnable-track {
  background: linear-gradient(#ccc, #ccc) var(--sx) 100% no-repeat #f0ad4e;
}
#data-speed-input::-webkit-slider-thumb {
  margin-top: -8px;
  box-sizing: border-box;
  border: none;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #f0ad4e;
}
#loader {
  border: 30px solid #faf3d1;
  border-top: 30px solid #f0ad4e;
  border-radius: 50%;
  width: 250px;
  height: 250px;
  animation: spin 1.5s linear infinite;
  margin: auto;
}
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
#loader-text {
  margin-top: 15px;
	font-size: 26px;
  color: #faf3d1;
}
#container {
  width: 100%;
  height: 100%;
}

/* game-controls */
#game-controls {
  width: 95%;
  margin: 8px auto 0 auto;
  opacity: 0.5;
  transition: opacity 0.2s;
}
#game-controls .row .panel {
  position: relative;
  color: #333;  
  height: 180px;
}

#main-game {
  padding-right: 5px;
}
#main-game .input-group:first-child {
  margin-bottom: 8px;
}
#main-game .input-group:first-child span.input-group-addon:first-child {
  padding: 0 18px;
}
span.input-group-addon {
  cursor: default; 
  user-select: none;
}
#account-balance .table {
  width: 75%;
  margin: -6px auto 0 auto;
}
#account-balance .table > thead > tr > th, #account-balance .table > tbody > tr > th, #account-balance .table > thead > tr > td, #account-balance .table > tbody > tr > td {
  border-top: 0;
}
#account-balance .table > thead > tr > th, #account-balance .table > tbody > tr > th {
  font-weight: 400;
}
#account-balance .table tr:last-child {
  border-top: 5px double #ddd;
}
#account-balance .table tr:last-child > th, #account-balance .table tr:last-child > td {
  font-weight: 700;  
}

#game-history {
  padding-left: 5px;
}
#game-history .panel {
  border: 2px solid #ccc; 
}
#game-history .panel, #game-history .panel .panel-body {
  width: 100%;
  height: 100%; 
  margin: 0;
  padding: 0;   
}
#game-history table {
  width: 100%;
  height: 100%;
  border: none;
  font-size: 12px;
}
#game-history table tbody {
  display: block;
  height: 112px;
  overflow-y: scroll;
}
#game-history table tbody::-webkit-scrollbar { width: 2px; }
#game-history table tbody::-webkit-scrollbar-track { background: rgba(0, 0, 0, 0.2); }
#game-history table tbody::-webkit-scrollbar-thumb { background: rgba(0, 0, 0, 0.4); }
#game-history table thead tr, #game-history table tbody tr, #game-history table tfoot tr {
    display: table;
    width: 100%;
    table-layout: fixed;
}
#game-history table thead tr, #game-history table tfoot tr {
    width: calc( 100% - 2px ); /* remove scrollbar width */
}
#game-history table tr:first-child th { border-top: 0; }
#game-history table tr td:first-child, #game-history table tr th:first-child { border-left: 0; }
#game-history table tr td:last-child, #game-history table tr th:last-child { border-right: 0; }
#game-history table.table > thead > tr > th { text-align: center; height: 30px; cursor: default; }
#game-history table.table > tbody > tr > td { vertical-align: middle; position: relative; top: 1px; height: 27px; cursor: default; }
#game-history table.table > tfoot > tr > td { 
  border-top: 5px double #ccc;
  border-bottom: 0;
  border-left: 0;
  border-right: 0;
  font-weight: bold;  
  height: 30px;
  cursor: default;
}

#buy-sell-buttons {
  margin-top: 18px;
}
#buy, #sell {
  display: block;
  width: 100%;
  font-size: 20px;
  padding: 8px;
}

/* Tooltip */
[data-tooltip] {
  position: relative;
}
[data-tooltip]:before, [data-tooltip]:after {
  position: absolute;
  visibility: hidden;
  opacity: 0;
  pointer-events: none;
  transition: all 0.15s cubic-bezier(0.5, 1, 0.25, 1);
  z-index: 2;
}
[data-tooltip]:before {
  padding: 5px;
  width: 110px;
  border-radius: 3px;
  background: rgba(0, 0, 0, 0.9);
  color: #fff;
  content: attr(data-tooltip);
  text-align: center;
  font-size: 12px;
  font-weight: normal;
  line-height: 1.2;
  white-space: normal;  
}
[data-tooltip]:after {
  border: 5px solid transparent;
  width: 0;
  content: "";
  font-size: 0;
  line-height: 0;
}
[data-tooltip]:hover:before, [data-tooltip]:hover:after {
  visibility: visible;
  opacity: 1;
}
[data-tooltip].t-xl:before { width: 200px; }
[data-tooltip].t-lg:before { width: 170px; }
[data-tooltip].t-md:before { width: 140px; }
[data-tooltip].t-sm:before { width: 100px; }
[data-tooltip].t-xs:before { width: 80px; }
[data-tooltip].t-top:before {
  bottom: 100%;
  left: 50%;
  margin-bottom: 5px;
  transform: translateX(-50%);
}
[data-tooltip].t-top:after {
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-top: 5px solid rgba(0, 0, 0, 0.9);
  border-bottom: none;
}
[data-tooltip].t-top:hover:before, [data-tooltip].t-top:hover:after {
  transform: translateX(-50%) translateY(-5px);
}
[data-tooltip].t-right:before {
  top: 50%;
  left: 100%;
  margin-left: 5px;
  transform: translateY(-50%);
}
[data-tooltip].t-right:after {
  top: 50%;
  left: 100%;
  transform: translateY(-50%);
  border-right: 5px solid rgba(0, 0, 0, 0.9);
  border-left: none;
}
[data-tooltip].t-right:hover:before, [data-tooltip].t-right:hover:after {
  transform: translateX(5px) translateY(-50%);
}
[data-tooltip].t-bottom:before {
  top: 100%;
  left: 50%;
  margin-top: 5px;
  transform: translateX(-50%);
}
[data-tooltip].t-bottom:after {
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border-bottom: 5px solid rgba(0, 0, 0, 0.9);
  border-top: none;
}
[data-tooltip].t-bottom:hover:before, [data-tooltip].t-bottom:hover:after {
  transform: translateX(-50%) translateY(5px);
}
[data-tooltip].t-left:before {
  top: 50%;
  right: 100%;
  margin-right: 5px;
  transform: translateY(-50%);
}
[data-tooltip].t-left:after {
  top: 50%;
  right: 100%;
  transform: translateY(-50%);
  border-left: 5px solid rgba(0, 0, 0, 0.9);
  border-right: none;
}
[data-tooltip].t-left:hover:before, [data-tooltip].t-left:hover:after {
  transform: translateX(-5px) translateY(-50%);
}

@media (max-width: 1200px) {
  #main-game, #game-history {  padding-right: 10px; padding-left: 10px; }
  #game-history { margin-top: -10px; margin-bottom: 0px; }
}
@media (min-height: 800px) {
  #game-controls { margin: 20px auto; }
  #main-game, #game-history { padding-right: 15px; padding-left: 15px; }
  #chart-section-container { margin-top: 15px; }
}
@media (max-width: 768px) {
  body { height: 100vh; } 
  #chart-section-container { height: 50%; margin-bottom: 2px; }
  #loader { width: 200px; height: 200px; }  
  #loader-text { font-size: 22px; }
  #data-speed-input { top: 3px; width: 90px; right: 40px; --sx: calc((var(--ratio)*90+9)*var(--px)); }
  #data-speed-input::-webkit-slider-runnable-track { width: 90px; height: 4px; }
  #data-speed-input::-webkit-slider-thumb { margin-top: -7px; width: 18px; height: 18px; }
  .chart-buttons-container button.btn-sm { font-size: 12px; padding: 3px 8px; }
  #refresh-btn, #show-hide-asset { margin-left: 5px; }
  #game-controls { margin: 8px auto 0 auto; }
  #game-controls .row .panel { height: 142px; }
  #main-game, #game-history {  padding-right: 15px; padding-left: 15px; }
  #main-game { font-size: 12px; }
  #main-game .panel-body { padding: 9px 12px; }
  #main-game .input-group { font-size: 10px; padding: 0; }
  #main-game .input-group-addon { font-size: 8px; padding: 5px; }
  #main-game .input-group:first-child span.input-group-addon:first-child { padding: 0 8px; }
  #account-balance .table { width: 100%; margin: 0 auto; font-size: 10px; }
  #account-balance .table tr:last-child { border-top: 3px double #ddd; }
  #account-balance .table-condensed > thead > tr:last-child > th, #account-balance .table-condensed > tbody > tr:last-child > th, #account-balance.table-condensed > thead > tr:last-child > td, .table-condensed > tbody > tr:last-child > td { padding-top: 8px; }
  #game-history table { font-size: 6px; }
  #game-history table tbody { height: 96px; }
  #game-history table.table > thead > tr > th { height: 23px; }
  #game-history table.table > tbody > tr > td { height: 23px; }
  #game-history table.table > tfoot > tr > td { height: 16px; }  
  #game-history table.table.table-condensed > tbody > tr > td { padding: 5px 2px; }  
  #game-history table.table.table-condensed > tfoot > tr > td { padding: 3px 2px 1px 2px; } 
  #buy-sell-buttons { margin-top: 10px; }
  #buy, #sell { font-size: 16px; padding: 5px; }  
  [data-tooltip]:before { font-size: 10px; } 
  [data-tooltip].t-sm:before { width: 76px; }
  [data-tooltip].t-xs:before { width: 70px; }
}

/* Animations */
.tada { animation: tada 1s both; }
@keyframes tada {
  from { transform: scale3d(1, 1, 1); }
  10%, 20% { transform: scale3d(.9, .9, .9) rotate3d(0, 0, 1, -3deg); }
  30%, 50%, 70%, 90% { transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, 3deg); }
  40%, 60%, 80% { transform: scale3d(1.1, 1.1, 1.1) rotate3d(0, 0, 1, -3deg); }
  to { transform: scale3d(1, 1, 1); }
}
.bounceIn { animation: bounceIn 0.75s both; }
@keyframes bounceIn {
  from, 20%, 40%, 60%, 80%, to { animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000); }
  0% { opacity: 0; transform: scale3d(.3, .3, .3); }
  20% { transform: scale3d(1.1, 1.1, 1.1); }
  40% { transform: scale3d(.9, .9, .9); }
  60% { opacity: 1; transform: scale3d(1.03, 1.03, 1.03); }
  80% { transform: scale3d(.97, .97, .97); }
  to { opacity: 1; transform: scale3d(1, 1, 1); }
}

/* Highcharts Configuration */
.highcharts-candlestick-series .highcharts-point { fill: #ff3333; }
.highcharts-candlestick-series .highcharts-point-up { fill: #33ff33; }
.highcharts-title { opacity: 0; transition: opacity 0.2s; }
</style>

  
  
  
  

</head>

<body translate="no" >
  <div id="chart-section-container">

  <div id="loader-section" class="text-center">
      <div id="loader"></div>
      <p id="loader-text">Loading data...</p>
  </div>		

  <div class="chart-buttons-container" id="chart-buttons-container-left">
    <button id="start-end-game" class="btn btn-success btn-sm"><i class="glyphicon glyphicon-off"></i></button>
    <button id="refresh-btn" class="btn btn-warning btn-sm"><i class="glyphicon glyphicon-refresh"></i></button>
    <button id="show-hide-asset" class="btn btn-warning btn-sm"><i class="glyphicon glyphicon-eye-open"></i></button>  
  </div>  

  <div class="chart-buttons-container" id="chart-buttons-container-right">
    <input id="data-speed-input" type="range" min="1" max="20" step="1" value="10" style="--val: 10;">
    <button id="play-pause" class="btn btn-warning btn-sm"><i class="glyphicon glyphicon-play"></i></button>  
  </div>

  <div id="container"></div>  

</div>

<div id="game-controls" class="text-center">
  <div class="row">

    <div id="main-game" class="col-xs-12 col-lg-6">
      <div class="panel">
        <div class="panel-body">
         <div class="row">
            <div class="col-xs-6 text-left">
              <div class="input-group">
                <span class="input-group-addon t-top t-sm" data-tooltip="Place your bet!">Amount:</span>
                <input id="betting-amount" type="number" class="form-control" placeholder="..." value=1000 min="0" max="100000" step="1000">   
                <span class="input-group-addon">$</span>
              </div>
              <div class="input-group">
                <span class="input-group-addon t-bottom t-xs" data-tooltip="Maturity (data points)">Expires in:</span>
                <input id="expiry" type="number" class="form-control" placeholder="..." value=10 min="1" max="100" step="1">  
                <span class="input-group-addon">#</span>
              </div>              
            </div>
            <div id="account-balance" class="col-xs-6 text-left">
              <table class="table table-condensed">
                <tr>
                  <th>Cash Balance:</th>
                  <td class="text-left">$<span id="cash-balance">100,000</span></td>
                </tr>
                <tr>
                  <th>Open Positions:</th>
                  <td>$<span id="open-positions">0</span></td>
                </tr>
                <tr>
                  <th>Equity:</th>
                  <td>$<span id="equity">100,000</span></td>
                </tr>
              </table>              
            </div>           
          </div>

          <div class="row" id="buy-sell-buttons">
            <div class="col-xs-6">          
              <button id="buy" class="btn btn-success">Buy</button>
            </div>
            <div class="col-xs-6">          
              <button id="sell" class="btn btn-danger">Sell</button>
            </div>            
          </div>
        </div>   
      </div>  
    </div> <!--/ #main-game -->

    <div id="game-history" class="col-xs-12 col-lg-6">
      <div class="panel">
        <div class="panel-body">
          <table class="table table-bordered table-hover table-condensed">
            <thead>
              <tr>
                <th>Order (#)</th>
                <th>Time</th>
                <th>Price ($)</th>
                <th>Type</th>
                <th>Amount ($)</th>
                <th>Time</th>
                <th>Price ($)</th>
                <th>Profit ($)</th>   
              </tr>
            </thead>
            <tbody>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
              </tr>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
              </tr>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
              </tr>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
              </tr>  
            </tbody>
            <tfoot>
              <tr class="active">
                <td colspan="2">Win Rate: <span id="win-rate">0/0</span></td>
                <td colspan="2">Avg. Profit: $<span id="average-profit">0</span></td>
                <td colspan="2">Avg. Loss: $<span id="average-loss">0</span></td>
                <td colspan="2">Profit: <span id="total-profit">$0</span></td>               
              </tr>               
            </tfoot>
          </table>          
        </div>
      </div>
    </div> <!--/ #game-history -->

  </div>
</div>
  
  <script src='https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/js/bootstrap.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/jqueryui/1.12.1/jquery-ui.min.js'></script>
<script src='https://code.highcharts.com/stock/highstock.js'></script>
      <script id="rendered-js" >
// Global Variables
const proxyURL = "https://cors-anywhere.herokuapp.com/"; // This is in order to bypass the 'Access-Control-Allow-Origin' error
const QUANDL_API_KEY = "HUNY3ZLcWGwrqcPJkihf"; // The Quandl API Key
const assets = ["AAPL", "ACCL", "AIRM", "AIT", "AKS", "AMZN", "ARTNA", "ASPS", "BCRX", "BIOL", "BLOX", "BMRN", "BSET", "BZH", "CASS", "CDI", "CE", "CFNL", "CHTR", "COVS", "CSCO", "CST", "CTIC", "CUR", "DMD", "DOC", "ENH", "ENTA", "ENZ", "ESIO", "ETH", "EVC", "FB", "FFKT", "FORR", "GAIA", "GB", "GCI", "GPX", "HL", "HOMB", "HPQ", "HTZ", "IDTI", "IHS", "IVC", "KEM", "KWR", "LWAY", "MA", "MBRG", "MCD", "MDCI", "MFRM", "MRIN", "MSFT", "MTG", "NBL", "NEOG", "NEWM", "NKE", "NWLI", "OHI", "PE", "PEIX", "PENN", "PENX", "PM", "PRSC", "PWR", "PZZA", "QLYS", "RBCAA", "RJET", "RNR", "ROL", "RRC", "SAIA", "SB", "SQI", "SRE", "SWY", "TAP", "TBPH", "TCB", "TECH", "THS", "TMO", "TOWR", "TPLM", "TRMB", "TSLA", "UDR", "UEIC", "UVV", "VAL", "VTG", "WBA", "WBC", "WWW"]; // 100 possible underlying assets
let asset = ""; // the underlying asset name eg. "AAPL" or "MSFT"
let displayedDataPoints = []; // Revealed data points
let remainingDataPoints = []; // Hidden data points
let chart; // The Main Chart
let dataFlowIntervalFunction; // The Data Flow Interval Function
let dataFlowIntervalTimer = Math.round((10/$("#data-speed-input").val())*1000); // The intervals (in milliseconds) on how often to execute the dataFlowIntervalFunction (min: 0.5s, max: 10s)
let isGamePaused = true; // isGamePaused boolean value
let isAssetHidden = true; // isAssetHidden boolean value
let isGameInProgress = false; // isGameInProgress boolean value
const initialCashBalance = 100000; // Initial Cash Balance
let gameHistory = { // Holds the game history and current state
  cashBalance: initialCashBalance,
  openPositions: 0,
  equity: initialCashBalance,
  totalBetsMatured: 0,
  totalBetsWon: 0,
  totalAmountWon: 0,
  totalAmountLost: 0,
  totalProfit: 0,
  history: []
};

drawChart(); // Draw Chart (default options)

// Handle the Start/End Game Button Click
$("#start-end-game").click(function(event) {
  if(isGameInProgress) { // end current game
    $("#start-end-game").removeClass("btn-danger").addClass("btn-success");
    $("#refresh-btn").prop("disabled", false);
    if(!isGamePaused) { $("#play-pause").click(); }    
    $("#game-controls").css("opacity", 0.5);
    isGameInProgress = !isGameInProgress;
  }
  else { // initiate game
    if(remainingDataPoints.length>0) {
      if(gameHistory.history.length>0) { clearPreviousGame(); }
      $("#start-end-game").removeClass("btn-success").addClass("btn-danger");
      $("#refresh-btn").prop("disabled", true);
      if(isGamePaused) { $("#play-pause").click(); }
      $("#game-controls").css("opacity", 1);  
      isGameInProgress = !isGameInProgress;
    }
    else {
      $("#refresh-btn").addClass("tada");
      setTimeout(function(){ $("#refresh-btn").removeClass("tada"); }, 1000);
    }
  }    
});

// Handle the Show/Hide Asset Button Click
$("#show-hide-asset").click(function(event){
  if(isAssetHidden) { 
    $("#show-hide-asset i").removeClass("glyphicon-eye-open").addClass("glyphicon-eye-close");
    $(".highcharts-title").css("opacity", 1);
    chart.series[0].update({name: asset.toUpperCase()}, false);
  }
  else {
    $("#show-hide-asset i").removeClass("glyphicon-eye-close").addClass("glyphicon-eye-open");
    $(".highcharts-title").css("opacity", 0);
    chart.series[0].update({name: 'Series 1'}, false);
  }
  isAssetHidden = !isAssetHidden;
});

// Handle "play-pause" click
$("#play-pause").click(function(event){
  if(isGamePaused) { // Continue data flow
    $("#play-pause i").removeClass("glyphicon-play").addClass("glyphicon-pause");
    dataFlowIntervalFunction = setInterval(() => addDataPoint(), dataFlowIntervalTimer);     
  }
  else { // Pause data flow
    $("#play-pause i").removeClass("glyphicon-pause").addClass("glyphicon-play");
    clearInterval(dataFlowIntervalFunction);
  }
  isGamePaused = !isGamePaused;
});

// Handle the Refresh Button Click (get asset data and draw chart)
$("#refresh-btn").click(function(event){
  if(gameHistory.history.length>0) { clearPreviousGame(); }
  drawChart();
  if(!isGamePaused) {
    $("#play-pause").click(); 
  }
  else {
    if($("#play-pause").prop("disabled")) { $("#play-pause").prop("disabled", false); }
  }
});

// Handle "data-speed-input" change event
$("#data-speed-input").on("input", function() {
  $(this).attr("style",`--val: ${$(this).val()};`);
  dataFlowIntervalTimer = Math.round((10/$(this).val())*1000);
  if(!isGamePaused) {
    clearInterval(dataFlowIntervalFunction);
    dataFlowIntervalFunction = setInterval(() => addDataPoint(), dataFlowIntervalTimer);
  }
});

// Handle "#betting-amount" blur event
$("#betting-amount").blur(function(){
  if(+$(this).attr("max")<+$(this).val()) {
    $(this).val($(this).attr("max"));
  }
});
// Handle "#expiry" blur event
$("#expiry").blur(function(){
  if(+$(this).attr("max")<+$(this).val()) {
    $(this).val($(this).attr("max"));
  }
});

// Handle buy/sell click
$("#buy-sell-buttons button").click(function(event){
  if(!isGameInProgress) { 
    $("#start-end-game").addClass("tada");
    setTimeout(function(){ $("#start-end-game").removeClass("tada"); }, 1000);
    return; 
  }
  const action = event.target.id;
  const bettingAmount = round(Math.min(+$("#betting-amount").val(), +$("#betting-amount").attr("max")), 0);
  const expiry = Math.min(+$("#expiry").val(), +$("#expiry").attr("max"));
  const betID = gameHistory.history.length + 1;
  const dateOptions = {year: "numeric", month: "short", day: "numeric"};
  if(bettingAmount>0 && expiry>0) {
    gameHistory.cashBalance-=bettingAmount;
    gameHistory.openPositions+=bettingAmount;
    gameHistory.history.push({
      id: betID,
      action: action,
      bettingAmount: bettingAmount,
      startingIndex: displayedDataPoints.length-1,
      startingTimeStamp: new Date(displayedDataPoints[displayedDataPoints.length-1][0]),
      startingPrice: displayedDataPoints[displayedDataPoints.length-1][4],
      expiryIndex: displayedDataPoints.length-1 + expiry,
      expiryTimeStamp: new Date(remainingDataPoints[expiry-1][0]),
      expiryPrice: remainingDataPoints[expiry-1][4],
      profit: action==="buy" ? (+displayedDataPoints[displayedDataPoints.length-1][4] < +remainingDataPoints[expiry-1][4] ? bettingAmount : -bettingAmount) : (+displayedDataPoints[displayedDataPoints.length-1][4] > +remainingDataPoints[expiry-1][4] ? bettingAmount : -bettingAmount)
    });
    $("#game-history table tbody").prepend(`<tr id="bet-${gameHistory.history[gameHistory.history.length-1].id}">
                                              <td>${gameHistory.history.length}</td>
                                              <td>${gameHistory.history[gameHistory.history.length-1].startingTimeStamp.toLocaleDateString("en-US", dateOptions)}</td>
                                              <td>${numberToText(gameHistory.history[gameHistory.history.length-1].startingPrice)}</td>
                                              <td>${gameHistory.history[gameHistory.history.length-1].action}</td>
                                              <td>${numberToText(gameHistory.history[gameHistory.history.length-1].bettingAmount)}</td>
                                              <td>${gameHistory.history[gameHistory.history.length-1].expiryTimeStamp.toLocaleDateString("en-US", dateOptions)}</td>
                                              <td></td>
                                              <td></td>
                                            </tr>`);
    if(betID<=4) { $("#game-history table tbody tr").last().remove(); }
    $("#cash-balance").text(numberToText(gameHistory.cashBalance));
    $("#open-positions").text(numberToText(gameHistory.openPositions));
    $("#betting-amount").attr("max", gameHistory.cashBalance);
    if(+$("#betting-amount").val()%1 != 0) { $("#betting-amount").val(bettingAmount); } // If input value decimal -> replace with integer
    $("#betting-amount").blur();
  }
});

/*
// Auxiliary Functions
*/

// Get data and create the chart 
function drawChart() {
  $("#container").hide();
  $(".chart-buttons-container").hide();
  $("#loader-section").show();
  asset = assets[Math.floor(Math.random()*assets.length)];
  $.getJSON(proxyURL + "https://www.quandl.com/api/v3/datasets/WIKI/" + asset + "/data.json?api_key=" + QUANDL_API_KEY, function(rawData) {
    const data = processRawData(rawData);
    generateDataArrays(data); // generate the arrays of "displayedDataPoints" and "remainingDataPoints"
    // create the chart
    chart = Highcharts.stockChart('container', { 
      rangeSelector: {
        buttons: [{type: 'month',count: 1,text: '1m'}, {type: 'month',count: 3,text: '3m'}, {type: 'month',count: 6,text: '6m'}, {type: 'year',count: 1,text: '1y'}, {type: 'all',text: 'All'}],
        selected: window.innerWidth>768 ? 3 : 2
        // inputEnabled: false
      },   
      title: {
        text: asset,
        margin: 8   
      },     
      xAxis: {
        crosshair: true
      },
      yAxis: {
        crosshair: true
      },      
      series: [{
        type: 'candlestick',     
        name: isAssetHidden ? 'Series 1' : asset,
        data: displayedDataPoints,
        dataGrouping: {
          units: [
            ['day', [1] ]
          ]
        }
      }]
    });
    isAssetHidden ? $(".highcharts-title").css("opacity", 0) : $(".highcharts-title").css("opacity", 1);
    setTimeout(function(){
      $("#loader-section").hide();
      $("#container").show();    
      $(".chart-buttons-container").show();
    }, 500);
  })
  .fail(function( jqxhr, textStatus, error ) {
      const err = textStatus + ", " + error;
      console.log( "Request Failed: " + err );
  });    
}

// Process Raw Data from API to a "working" data format
function processRawData(rawData) {
  rawData = rawData.dataset_data.data;
  let data = [];
  for(let i=0; i<rawData.length; i++) {
    let dataRow = [];
    dataRow.push(Date.parse(rawData[i][0]));
    for(let j=1; j<5; j++) {
      dataRow.push(rawData[i][j]);
    }
    data.push(dataRow);
  }
  data.reverse(); // Ascending Order for Dates (raw data comes in descending order)
  return data;
}

// Generate the arrays of "displayedDataPoints" and "remainingDataPoints" (by randomly selecting the "break" point)
function generateDataArrays(data) {
  const maxDisplayedIndex = data.length > 300 ? data.length-300 : 0; // Leave at least 300 hidden data points (or all points if less than 300 points available)
  const randomDisplayedIndex = Math.floor(Math.random()*maxDisplayedIndex);
  displayedDataPoints = [];
  remainingDataPoints = [];
  for(let i=0; i<randomDisplayedIndex; i++) displayedDataPoints.push(data[i]);
  for(let i=randomDisplayedIndex; i<data.length; i++) remainingDataPoints.push(data[i]);
}

// Add data point to Chart
function addDataPoint() {
  if(remainingDataPoints.length>0) {
    chart.series[0].addPoint(remainingDataPoints.shift()); // addPoint(options [,redraw] [,shift])
    if(remainingDataPoints.length<+$("#expiry").attr("max")) { 
      $("#expiry").attr("max", remainingDataPoints.length); 
      $("#expiry").blur();
    }
    checkForExpiredOpenPositions();
  }
  else { // Game Over...
    if(isGameInProgress){ $("#start-end-game").click(); }
    else { $("#play-pause").click(); }
    $("#play-pause").prop("disabled", true);
  }
}

// Check for expired open potitions (after any added data point) and update gameHistory accordingly
function checkForExpiredOpenPositions() {
  const currentIndex = displayedDataPoints.length-1;
  const expiredIndexArray = []; // Currently expiring bets' indices (of gameHistory.history[])
  gameHistory.history.forEach((elem,index) => { if(elem.expiryIndex===currentIndex) expiredIndexArray.push(index); });
  if(expiredIndexArray.length>0) {
    // const expiryPrice = displayedDataPoints[currentIndex][4];  
    let closedPositionsAmount = 0;
    let closedPositionsProfit = 0;
    for(let i=0; i<expiredIndexArray.length; i++) {
      // gameHistory.history[expiredIndexArray[i]].expiryPrice = expiryPrice;
      closedPositionsAmount+=gameHistory.history[expiredIndexArray[i]].bettingAmount;
      closedPositionsProfit+=gameHistory.history[expiredIndexArray[i]].profit;
      $("#bet-"+gameHistory.history[expiredIndexArray[i]].id+" td").eq(-2).text(numberToText(gameHistory.history[expiredIndexArray[i]].expiryPrice));
      $("#bet-"+gameHistory.history[expiredIndexArray[i]].id+" td").eq(-1).text(numberToText(gameHistory.history[expiredIndexArray[i]].profit));
      if(gameHistory.history[expiredIndexArray[i]].profit>0) {
        $("#bet-"+gameHistory.history[expiredIndexArray[i]].id).addClass("success");
        gameHistory.totalBetsWon++;
        gameHistory.totalAmountWon += gameHistory.history[expiredIndexArray[i]].profit;
      } 
      else {
        $("#bet-"+gameHistory.history[expiredIndexArray[i]].id).addClass("danger");
        gameHistory.totalAmountLost += Math.abs(gameHistory.history[expiredIndexArray[i]].profit);        
      }
    }
    gameHistory.cashBalance += (closedPositionsAmount + closedPositionsProfit);
    gameHistory.openPositions -= closedPositionsAmount;
    gameHistory.equity = gameHistory.cashBalance + gameHistory.openPositions;
    gameHistory.totalBetsMatured += expiredIndexArray.length;
    gameHistory.totalProfit += closedPositionsProfit;
    $("#cash-balance").text(numberToText(gameHistory.cashBalance));
    $("#open-positions").text(numberToText(gameHistory.openPositions));
    $("#equity").text(numberToText(gameHistory.equity));
    $("#win-rate").text(gameHistory.totalBetsWon + "/" + gameHistory.totalBetsMatured);
    if(gameHistory.totalBetsWon>0) { $("#average-profit").text(numberToText(round(gameHistory.totalAmountWon/gameHistory.totalBetsWon, 0))); }
    if(gameHistory.totalBetsMatured-gameHistory.totalBetsWon>0) { $("#average-loss").text(numberToText(round(gameHistory.totalAmountLost/(gameHistory.totalBetsMatured-gameHistory.totalBetsWon), 0))); } 
    $("#total-profit").text(gameHistory.totalProfit>=0 ? "$" + numberToText(gameHistory.totalProfit) : "-$" + numberToText(Math.abs(gameHistory.totalProfit))); 
    $("#betting-amount").attr("max", gameHistory.cashBalance);
    if(gameHistory.equity===0) { // Game Over...
      if(isGameInProgress){ $("#start-end-game").click(); }
    }
  }
}

// Game Over
// function gameOver() {
  // $("#start-end-game").click();
  // $("#play-pause").prop("disabled", true);
  // $("#buy-sell-buttons button").prop("disabled", true);
// }

// Clear Previous Game History
function clearPreviousGame() {
  gameHistory = {
    cashBalance: initialCashBalance,
    openPositions: 0,
    equity: initialCashBalance,
    totalBetsMatured: 0,
    totalBetsWon: 0,
    totalAmountWon: 0,
    totalAmountLost: 0,
    totalProfit: 0,
    history: []
  };  
  $("#cash-balance").text(numberToText(gameHistory.cashBalance));
  $("#open-positions").text(numberToText(gameHistory.openPositions));
  $("#equity").text(numberToText(gameHistory.equity)); 
  $("#win-rate").text(gameHistory.totalBetsWon + "/" + gameHistory.totalBetsMatured);
  $("#average-profit").text("0");
  $("#average-loss").text("0")
  $("#total-profit").text("$0"); 
  $("#betting-amount").attr("max", gameHistory.cashBalance);
  $("#betting-amount").attr("value", 1000);
  $("#betting-amount").val(1000);
  $("#expiry").attr("max", 100);
  $("#expiry").attr("value", 10);
  $("#expiry").val(10);
  $("#game-history table tbody").empty();
  for(let i=1; i<=4; i++) {
    $("#game-history table tbody").append(`<tr>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                              <td></td>
                                            </tr>`);     
  } 
}

// Convert text(which actually is a number with "," as thousands' seperators) to number
function textToNumber(txt) {
  return +txt.split(",").join("");
}
// Convert number to text(using "," as thousands' seperators)
function numberToText(num) {
  if(Math.abs(num)<1000) return num.toString();
  else {
    const intAndDecPart = num.toString().split(".");
    const intPart = intAndDecPart[0];
    let res="";
    let counter = 0;
    for(let i=intPart.length-1; i>0; i--) {
      res = intPart[i] + res;
      counter++;
      if(counter%3===0) res = "," + res;
    }
    res = intPart[0] + res;
    if(intAndDecPart.length===2) return res+"."+intAndDecPart[1];
    else return res;
  }
}
// Auxilliary Rounding Function
function round(value, decimals) {
  return Number(Math.round(value+'e'+decimals)+'e-'+decimals);
} // Note: decimals>=0, Example: round(1.005, 2); -> 1.01
    </script>

  

</body>

</html>
 
