<script lang="ts">
	let author: string;
	let text: string;
    let image_src: string;
    image_src = "https://pbs.twimg.com/profile_images/900272730460872705/Uo2qnt1H_400x400.jpg"
    
    author = "DW на русском";
    text = "Немецкий концерн Rheinmetall откроет в Румынии, рядом с украинской границей, ремонтный и логистический хаб для техобслуживания вооружений, поставляемых Украине, в том числе, немецких танков Leopard и британских Challenger. Об этом сообщает Reuters со ссылкой на саму компанию";
</script>

<div id="post">
    
    
    <div id="post-content-wrapper">
        <div id="photo-wrap">
            <div id="post-author-photo">
                <img id="photo" src={image_src} alt="profile avatar" />
            </div>
            <div id="post-author">
                <b>{author}</b>
            </div>
        </div>

        <div id="post-text">
            {text}
        </div>
        <div id="views-wrap">
            <div id="views">
                12,9 тыс. просмотров, 12:50
            </div>
        </div>

        <div id="activities">
            <div class="activity-text" id="likes">
                125 Like
            </div>
            <div class="activity-text" id="comments">
                365 Comments
            </div>
            <div class="activity-text" id="save">
                Save
            </div>
            <div class="activity-text" id="share">
                Share
            </div>
        </div>
        
    </div>
</div>




<style>
    
#photo-wrap{
    display: flex;
    flex-direction: row;
    justify-content: start;
}
#photo{
    width:100%;
    height:100%;
}
#views-wrap{
    width:200px;
    margin-top:5px;
    margin-left: auto;
    margin-right: 0em;
    margin-bottom: 0px;
}
#views{
    color: #363636;
    font-size: 16px;
    text-align: right;
}
#post{
    box-shadow: rgba(50, 50, 93, 0.10) 0px -10px 100px -20px, rgba(0, 0, 0, 0.07) 0px 30px 60px 10px;
    margin-top:15px;
    margin-bottom:15px;
    width:600px;
    
    background-color: white;
    border-radius: 10px;
}
#post-content-wrapper{
    padding-left: 30px;
    padding-right: 30px;
    padding-top: 10px;
    padding-bottom:10px;
}
#post-author{
    font-size: 20px;
    padding-top: 15px;
    padding-bottom: 15px;
    margin-left: 10px;
}
#post-author-photo{
    width:44px;
    height:44px;
    margin-top: 3px;
    margin-bottom: 3px;
    border-radius: 30px;
    background-color: red;
    overflow: hidden;
}
#post-text{
    
}
#activities{
    display: flex;
    flex-direction: row;
}
.activity-text{
    color: blue;
    padding-top:15px;
    margin-right:50px;
    padding-bottom:10px;
}
</style>