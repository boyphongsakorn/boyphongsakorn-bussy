<script>
  import { Styles,Card,Row,Col,Icon,Image,Container,Accordion,AccordionItem,Badge,Button } from 'sveltestrap/src';
  import Avatar from "svelte-avatar";
  let name = ''
  if(window.location.hostname.includes('pwisetthon')){
    name = 'พงศกร วิเศษธร (บอย)';
  }else{
    name = 'บริษัท ทีมควอดบี จำกัด';
  }
  console.log(window.location.hostname)
  let events = [['07-09-2022 09:00','07-09-2022 17:00','ขอนแก่น','cancel'],['07-31-2022 18:00','08-06-2022 18:00','นนทบุรี','cancel'],['09-03-2022 18:00','09-11-2022 08:00','นนทบุรี','cancel'],['10-02-2022 18:00','10-08-2022 08:00','นนทบุรี','cancel'],['10-29-2022 21:00','11-05-2022 08:00','นนทบุรี','goingon'],['11-12-2022 10:00','11-12-2022 17:00','ขอนแก่น','goingon'],['11-26-2022 23:00','12-3-2022 17:00','นนทบุรี','goingon'],['01-03-2023 21:00','01-06-2023 05:00','นนทบุรี','goingon'],['01-06-2023 05:00','01-08-2023 21:00','ภูเก็ต','goingon'],['01-08-2023 21:00','01-14-2023 12:00','นนทบุรี','goingon']]
  let imgsplist = ['https://res.cloudinary.com/dstnfzzu4/image/upload/v1602160097/teamquadb/fire_lqe3xv.png','https://res.cloudinary.com/dstnfzzu4/image/upload/v1626324277/quadb_lott/two-standing-smartphones-mockup_zwf7ls.png','https://res.cloudinary.com/dstnfzzu4/image/upload/v1602162255/teamquadb/120603592_3279839782114711_727098858267587641_o_qrduk3.jpg']
  async function getoutoldevents(levents){
    let now = new Date();
    let nowtime = now.getTime();
    let eventlist = [];
    for(let i=0;i<levents.length;i++){
      let start = new Date(levents[i][0]);
      let end = new Date(levents[i][1]);
      let starttime = start.getTime();
      let endtime = end.getTime();
      //let response = await fetch("https://anywhere.pwisetthon.com/https://province-thai-api.vercel.app");
      //let data = await response.json();
      //get provinceName by levents[i][2]
      //for(let j=0;j<data.length;j++){
      //  if(data[j].provinceName == levents[i][2]){
      //    levents[i][5] = data[j].sealUrl;
      //    break;
      //  }
      //}
      //if levents[i][2] == 'นนทบุรี' then levents[i][5] = 'https://img.gs/fhcphvsghs/120x120,crop/https://www.phuket.go.th/webpk/images/introduce/logo-phuket2565.jpg'
      if(levents[i][2] == 'ภูเก็ต'){
        levents[i][5] = 'https://img.gs/fhcphvsghs/120x120,crop/https://www.phuket.go.th/webpk/images/introduce/logo-phuket2565.jpg'
      }
      if(levents[i][2] == 'นนทบุรี'){
        levents[i][5] = 'https://img.gs/fhcphvsghs/99x120,crop/https://www.thebestcenter.com/wp-content/uploads/2021/07/logo210702063101.png'
      }
      console.log(nowtime)
      console.log(endtime)
      if((nowtime<=starttime || nowtime<=endtime) && levents[i][3] == 'goingon'){
        eventlist.push(levents[i]);
      }
    }
    return eventlist;
  }
  async function getoldevents(levents){
    let now = new Date();
    let nowtime = now.getTime();
    let eventlist = [];
    for(let i=0;i<levents.length;i++){
      let start = new Date(levents[i][0]);
      let end = new Date(levents[i][1]);
      let starttime = start.getTime();
      let endtime = end.getTime();
      let response = await fetch("https://anywhere.pwisetthon.com/https://province-thai-api.vercel.app");
      let data = await response.json();
      //get provinceName by levents[i][2]
      for(let j=0;j<data.length;j++){
        if(data[j].provinceName == levents[i][2]){
          levents[i][5] = data[j].sealUrl;
          break;
        }
      }
      if(nowtime>=starttime && nowtime>=endtime){
        eventlist.push(levents[i]);
      }
    }
    return eventlist;
  }
  function getmonth(mount){
    mount++;
    let month = ''
    switch(mount){
      case 1:
        month = 'มกราคม'
        break;
      case 2:
        month = 'กุมภาพันธ์'
        break;
      case 3:
        month = 'มีนาคม'
        break;
      case 4:
        month = 'เมษายน'
        break;
      case 5:
        month = 'พฤษภาคม'
        break;
      case 6:
        month = 'มิถุนายน'
        break;
      case 7:
        month = 'กรกฎาคม'
        break;
      case 8:
        month = 'สิงหาคม'
        break;
      case 9:
        month = 'กันยายน'
        break;
      case 10:
        month = 'ตุลาคม'
        break;
      case 11:
        month = 'พฤศจิกายน'
        break;
      case 12:
        month = 'ธันวาคม'
        break;
    }
    return month
  }
  function gettime(start,end) {
    let starttime = new Date(start);
    let endtime = new Date(end);
    //if starttime and endtime is same day
    if(starttime.getDate() == endtime.getDate()){
      if(starttime.getHours() == 0 && endtime.getHours() == 23){
        return 'ทั้งวัน'
      }
      return ('0' + starttime.getHours()).slice(-2) + ':' + ('0' + starttime.getMinutes()).slice(-2) + ' - ' + ('0' + endtime.getHours()).slice(-2) + ':' + ('0' + endtime.getMinutes()).slice(-2);
    }else{
      return 'วันที่ '+endtime.getDate()+' '+getmonth(endtime.getMonth())+' '+(endtime.getFullYear()+543)+' เวลา '+('0' + endtime.getHours()).slice(-2) + ':' + ('0' + endtime.getMinutes()).slice(-2);
    }
    //return 'test';
  }
  function getthaiformat(date){
    let time = new Date(date);
    return 'วันที่ '+time.getDate()+' '+getmonth(time.getMonth())+' '+(time.getFullYear()+543)+' เวลา '+('0' + time.getHours()).slice(-2) + ':' + ('0' + time.getMinutes()).slice(-2);
  }
</script>

<Styles />

<svelte:head>
  <title>ตารางงานของ {name}</title>
</svelte:head>

<Container>
  <Row>
    <Col sm="12" md={{ size: 6, offset: 3 }}>
      <Card class="mb-1" body><center><h2>ตารางงานของ {name}</h2></center></Card>
      <!--Card body><p class="mb-0"><Icon name="info-square-fill" /> ยังไม่มีตารางงานของ {name}</p></Card-->
      <a href="https://boyphongsakorn-book.vercel.app" class="text-decoration-none mb-1"><Button class="mb-1" block>จองคิว/จองเวลา</Button></a>
      <Accordion class="mb-1">
        <AccordionItem active header="งานประจำ วันจันทร์ถึงศุกร์">
          <!--Card body-->
          <p><Icon name="calendar-event" /> วันจันทร์ถึงศุกร์</p>
          <p style="display: inline-flex;"><Avatar src="https://www.m-culture.go.th/khonkaen/images/Khonkaen2016/khonkaenLogo.png" /> บ้าน</p>
          <p><Icon name="clock-fill" /> เวลา 09:00 ถึง 18:00</p>
          <!--/Card-->
        </AccordionItem>
        {#await getoutoldevents(events)}
          <Card body><p class="mb-0">กำลังโหลด......</p></Card>
        {:then list}
          {#each list as event, i}
            {#if list.length==0}
              <Card body><p class="mb-0">ยังไม่มีตารางงานของ {name}</p></Card>
            {/if}
            {#if i == 0}
              <AccordionItem header="{getthaiformat(event[0])} - {event[2]}">
                <!--Card body-->
                <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
                <p style="display: inline-flex;"><Avatar src={event[5]} /> {event[2]}</p>
                <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
                <!--/Card-->
              </AccordionItem>
            {:else}
              <AccordionItem header="{getthaiformat(event[0])} - {event[2]}">
                <!--Card body-->
                <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
                <p style="display: inline-flex;"><Avatar src={event[5]} /> {event[2]}</p>
                <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
                <!--/Card-->
              </AccordionItem>
            {/if}
          {/each}
        {:catch error}
          <Card body><p class="mb-0">Error...... F5 For Refresh</p></Card>
        {/await}
      </Accordion>
      <Accordion class="mb-1">
        <AccordionItem header="ตารางงานเก่า">
          {#await getoldevents(events)}
            <Card body><p class="mb-0">กำลังโหลด......</p></Card>
          {:then list}
            {#each list as event, i}
              <Card body>
                <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
                <p style="display: inline-flex;"><Avatar src={event[5]} /> {event[2]}</p>
                <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
              </Card>
            {/each}
          {:catch error}
            <Card body><p class="mb-0">Error...... F5 For Refresh</p></Card>
          {/await}
        </AccordionItem>
      </Accordion>
      {#each imgsplist as img}
      <div class="jsonArea rounded">
        <div class="buttonsGroup">
          <Badge color="danger">Sponsor</Badge>
        </div>
        <Image fluid alt="Landscape" src="https://img.gs/fhcphvsghs/1000x300,crop/{img}" />
      </div>
      {/each}
      <!--div style="position: relative;">
        <Image class="mt-1 rounded" fluid alt="Landscape" src="https://img.gs/fhcphvsghs/1000x300,crop/https://res.cloudinary.com/dstnfzzu4/image/upload/v1602160097/teamquadb/fire_lqe3xv.png" />
        <Badge color="danger" style="position: sticky;display: inline-block;float: right;">Sponsor</Badge>
      </div-->
      <!--Image class="mt-1 rounded" fluid alt="Landscape" src="https://img.gs/fhcphvsghs/1000x300,crop=top/" />
      <Image class="mt-1 rounded" fluid alt="Landscape" src="https://img.gs/fhcphvsghs/1000x300,crop/" /-->
    </Col>
  </Row>
</Container>

<style>
.buttonsGroup {
  position: sticky;
  display: inline-block;
  float: left;
  right: 0;
  height: 0;
  left: 5px;
  top: 5px;
}

.jsonArea {
  position: relative;
  overflow: auto;
  display: inline-block;
  width: 100%;
  background-color: #eeeeee;
  /*border-radius: 10px;
  -webkit-box-shadow: inset 0 0 12px rgba(0, 0, 0, 0.1);*/
}
</style>
