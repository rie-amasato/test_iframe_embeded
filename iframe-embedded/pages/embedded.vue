<template>
    <div>
        Cookie: {{int_cookie}}
    </div>

    <div>
        LocalStorage: {{int_locals}}
    </div>

    <div>
        SessionStorage: {{int_sessions}}
    </div>
</template>

<script setup>
const int_cookie=ref()
const int_locals=ref()
const int_sessions=ref()

setTimeout(()=>{// 画面描画後じゃないとCOOKIEなどが取れないので1msecまつ
   // COKIE
   const int_cookie_tes= parseInt(document.cookie.split("; ")
    .find((r)=>r.startsWith("tes"))
    ?.split("=")[1])+1
    
    document.cookie=`tes=${int_cookie_tes || 1};`
    int_cookie.value=int_cookie_tes;

    // LocalStorage
    try{
        const int_localsvalue=parseInt(localStorage.getItem("tes"))+1

        if (!isNaN(int_sessionsvalue)){
            localStorage.setItem("tes", int_localsvalue)

            int_locals.value=int_localsvalue
        else{
            localStorage.setItem("tes", 0)
        }

        console.log(int_localsvalue)
    }catch{
        console.log("catch")
        localStorage.setItem("tes",0)
    }
    
    // SessionStorage
    try{
        const int_sessionsvalue=parseInt(sessionStorage.getItem("tes"))+1
        if (!isNaN(int_sessionsvalue)){
            sessionStorage.setItem("tes", int_sessionsvalue)

            int_sessions.value=int_sessionsvalue
        }
        else{
            sessionStorage.setItem("tes", 0)
        }

        console.log(int_sessionsvalue)
    }catch{
        console.log("catch")
        sessionStorage.setItem("tes",0)
    }
},1)

</script>