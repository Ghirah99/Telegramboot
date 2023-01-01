var token = "";
var url = "https://api.telegram.org/bot" + token;
var webAppUrl = "";

function setWebhook() {
    var response = UrlFetchApp.fetch(url + "/setWebhook?url=" + webAppUrl);
    Logger.log(response.getContentText());
  }

function doPost(e) {
  var stringJson = e.postData.getDataAsString();
  var updates = JSON.parse(stringJson);

  var id = updates.message.from.id;
  var nama = updates.message.from.first_name;
  var text = " Hallo " + nama + ", Selamat datang diBot Percobaan !";


  sendText(id, text);

}


function sendText(chatid, text, replymarkup) {
  var data = {
    method: "post",
    payload: {
      method: "sendMessage",
      chat_id: String(chatid),
      text: text,
      parse_mode: "HTML",
      reply_markup: JSON.stringify(replymarkup)
    }
  };
  UrlFetchApp.fetch('https://api.telegram.org/bot' + token + '/', data);
}
