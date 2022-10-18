# chatapp_front

### 메세지 전송 js
``` javascript
async function addMessage(){
    let msgInput = document.querySelector("#chat-outgoing-msg");

    let chat = {
        sender: username,
        roomNum: roomNum,
        msg: msgInput.value
    };
    
    fetch(`${basicUrl}/chat`, {
        method: "post",
        body: JSON.stringify(chat),
        headers: {
            "Content-Type":"application/json; charset=utf-8"
        }
    })
    msgInput.value = "";
}
```

### 기존 메세지 받아오기
``` javascript
const eventSource = new EventSource(`${basicUrl}/chat/roomNum/${roomNum}`);

eventSource.onmessage = (event) => {
    const data = JSON.parse(event.data);
        getReceiveMsgBox(data);
}

function getReceiveMsgBox(data) {
    let md = data.createdAt.substring(5,10)
    let tm = data.createdAt.substring(11,16)
    convertTime = tm + " | " + md

    return `<div class="received_withd_msg">
    <p> ${data.msg} </p>
    <span class="time_date"> ${convertTime} / ${data.sender} </span>
  </div>`;
}
```