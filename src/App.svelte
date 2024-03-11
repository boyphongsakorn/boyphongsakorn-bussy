<script>
  import { Styles,Card,Row,Col,Icon,Image,Container,Accordion,AccordionItem,Badge,Button } from 'sveltestrap/src';
  import Avatar from "svelte-avatar";
  let name = ''
  if(window.location.hostname.includes('pwisetthon')){
    name = 'พงศกร วิเศษธร (บอย)';
  }else{
    // name = 'บริษัท ทีมควอดบี จำกัด';
    name = 'ทีมควอดบี'
  }
  console.log(window.location.hostname)
  let events = [
    ['07-09-2022 09:00','07-09-2022 17:00','ขอนแก่น','ขอนแก่น','cancel'],
    ['07-31-2022 18:00','08-06-2022 18:00','นนทบุรี','นนทบุรี','cancel'],
    ['09-03-2022 18:00','09-11-2022 08:00','นนทบุรี','นนทบุรี','cancel'],
    ['10-02-2022 18:00','10-08-2022 08:00','นนทบุรี','นนทบุรี','cancel'],
    ['10-29-2022 21:00','11-05-2022 08:00','นนทบุรี','นนทบุรี','goingon'],
    ['11-12-2022 10:00','11-12-2022 17:00','ขอนแก่น','ขอนแก่น','goingon'],
    ['11-26-2022 23:00','12-03-2022 17:00','นนทบุรี','นนทบุรี','goingon'],
    ['01-03-2023 21:00','01-06-2023 05:00','นนทบุรี','นนทบุรี','goingon'],
    ['01-06-2023 05:00','01-08-2023 21:00','ภูเก็ต','ภูเก็ต','goingon'],
    ['01-08-2023 21:00','01-14-2023 12:00','นนทบุรี','นนทบุรี','goingon'],
    ['03-11-2023 21:00','03-13-2023 21:00','นนทบุรี','นนทบุรี','goingon'],
    ['04-02-2023 23:00','04-07-2023 06:00','นนทบุรี','นนทบุรี','goingon'],
    ['06-10-2023 09:00','06-10-2023 18:00','ขอนแก่น','ขอนแก่น','goingon'],
    ['06-11-2023 12:00','06-17-2023 12:00','นนทบุรี','นนทบุรี','goingon'],
    ['06-17-2023 12:00','06-24-2023 12:00','นนทบุรี','นนทบุรี','goingon'],
    ['06-24-2023 12:00','07-08-2023 12:00','นนทบุรี','นนทบุรี','goingon'],
    ['11-18-2023 09:00','11-22-2023 20:00','กรุงเทพ','กรุงเทพ','goingon'],
    ['12-03-2023 11:00','12-16-2023 06:00','นนทบุรี','นนทบุรี','goingon']
  ]
  let imgsplist = ['https://res.cloudinary.com/dstnfzzu4/image/upload/v1602160097/teamquadb/fire_lqe3xv.png','https://res.cloudinary.com/dstnfzzu4/image/upload/v1626324277/quadb_lott/two-standing-smartphones-mockup_zwf7ls.png','https://res.cloudinary.com/dstnfzzu4/image/upload/v1602162255/teamquadb/120603592_3279839782114711_727098858267587641_o_qrduk3.jpg']
  async function getoutoldevents(levents){
    let now = new Date();
    let nowtime = now.getTime();
    let eventlist = [];
    let calfromapple = await fetch("https://anywhere.pwisetthon.com/https://p132-caldav.icloud.com/published/2/MTAzNzA0NDExMTMxMDM3MCr9RGds7qxF_lkSVxDFXqTqPU1HQUnSSsmFt97BXngD");
    let calfromappletext = await calfromapple.text();
    //split every event by BEGIN:VEVENT
    let calfromapplelist = calfromappletext.split('BEGIN:VEVENT');
    //push to levents by [DTSTART;,DTEND;,SUMMARY;,'goingon']
    for(let i=1;i<calfromapplelist.length;i++){
      let event = calfromapplelist[i].split('\n');
      // console.log(event)
      // let start = event[4].split(';')[1];
      // //if have DESCRIPTION: and next line is don't have :
      // if(event[2].includes('DESCRIPTION:')){
      //   //find line after that have :
      //   for(let j=3;j<event.length;j++){
      //     if(event[j].includes(':')){
      //       start = event[j+2].split(';')[1];
      //       break;
      //     }
      //   }
      // }
      // // alert(start)
      // //if start is VALUE=DATE then get after : and get index mm-dd-yyyy 00:00
      // if(start.includes('VALUE=DATE')){
      //   start = start.split(':')[1];
      //   start = start.slice(4,6)+'-'+start.slice(6,8)+'-'+start.slice(0,4)+' 00:00';
      // } else if(start.includes('TZID=Asia/Bangkok')){
      //   start = start.split(':')[1];
      //   //convert unix (yyyymmddThhmmss) to mm-dd-yyyy hh:mm
      //   start = start.slice(4,6)+'-'+start.slice(6,8)+'-'+start.slice(0,4)+' '+start.slice(9,11)+':'+start.slice(11,13);
      // }
      // let end = event[2].split(';')[1];
      // //if have DESCRIPTION: and next line is don't have :
      // if(event[2].includes('DESCRIPTION:')){
      //   //find line after that have :
      //   for(let j=3;j<event.length;j++){
      //     if(event[j].includes(':')){
      //       end = event[j].split(';')[1];
      //       break;
      //     }
      //   }
      // }
      // //if end is VALUE=DATE then get after : and get index mm-dd-yyyy 00:00
      // if(end.includes('VALUE=DATE')){
      //   end = end.split(':')[1];
      //   end = end.slice(4,6)+'-'+end.slice(6,8)+'-'+end.slice(0,4)+' 00:00';
      //   //cal from start to end if 1 day then end = start 23:59
      //   let startdate = new Date(start);
      //   let enddate = new Date(end);
      //   let startdatetime = startdate.getTime();
      //   let enddatetime = enddate.getTime();
      //   if((enddatetime-startdatetime)/86400000 == 1){
      //     end = start.slice(0,11)+'23:59';
      //   }
      // } else if(end.includes('TZID=Asia/Bangkok')){
      //   end = end.split(':')[1];
      //   //convert unix (yyyymmddThhmmss) to mm-dd-yyyy hh:mm
      //   end = end.slice(4,6)+'-'+end.slice(6,8)+'-'+end.slice(0,4)+' '+end.slice(9,11)+':'+end.slice(11,13);
      //   //cal from start to end if 1 day then end = start 23:59
      //   let startdate = new Date(start);
      //   let enddate = new Date(end);
      //   let startdatetime = startdate.getTime();
      //   let enddatetime = enddate.getTime();
      //   if((enddatetime-startdatetime)/86400000 == 1){
      //     end = start.slice(0,11)+'23:59';
      //   }
      // }
      // // alert('ok1')
      // let summary = event[8].includes('SUMMARY') ? event[8].split(':')[1] : event[7].split(':')[1];
      // if(event[2].includes('DESCRIPTION:')){
      //   //find line after that have :
      //   for(let j=3;j<event.length;j++){
      //     if(event[j].includes(':')){
      //       if(event[j+8].includes('SUMMARY')){
      //         summary = event[j+6].split(':')[1];
      //       }else{
      //         summary = event[j+5].split(':')[1];
      //       }
      //       break;
      //     }
      //   }
      // }
      // alert('ok2')
      // loop event
      let start,end,summary,location;
      for(let j=0;j<event.length;j++){
        if(event[j].includes('LOCATION')){
          // location = event[j].split(':')[1];
          // if start with https:// then location = ''
          // if(event[j].split(':')[1].includes('https://')){
          //   location = '';
          // }else{
            // location = event[j].split(':')[1];
          // }
          if(event[j].includes(':')) {
            if(event[j].split(':')[1].includes('https')){
              location = '';
            }else{
              location = event[j].split(':')[1];
              
              let provinceapi = (await fetch("https://raw.githubusercontent.com/kongvut/thai-province-data/master/api_province.json")).json();
              let province = await provinceapi;
              let locationbefore = location;
              for(let k=0;k<province.length;k++){
                if(province[k].name_en == location.trim()){
                  location = province[k].name_th;
                  break;
                }
              }
              for(let k=0;k<province.length;k++){
                if(location.trim().includes(province[k].name_en)){
                  location = province[k].name_th;
                  break;
                }
              }
            }
          }
        }
        if(event[j].includes('DTSTART;')){
          start = event[j].split(';')[1];
          if(start.includes('VALUE=DATE')){
            start = start.split(':')[1];
            start = start.slice(4,6)+'-'+start.slice(6,8)+'-'+start.slice(0,4)+' 00:00';
          } else if(start.includes('TZID=Asia/Bangkok')){
            start = start.split(':')[1];
            start = start.slice(4,6)+'-'+start.slice(6,8)+'-'+start.slice(0,4)+' '+start.slice(9,11)+':'+start.slice(11,13);
          }
        }
        if(event[j].includes('DTEND;')){
          end = event[j].split(';')[1];
          if(end.includes('VALUE=DATE')){
            end = end.split(':')[1];
            end = end.slice(4,6)+'-'+end.slice(6,8)+'-'+end.slice(0,4)+' 00:00';
            let startdate = new Date(start);
            let enddate = new Date(end);
            let startdatetime = startdate.getTime();
            let enddatetime = enddate.getTime();
            if((enddatetime-startdatetime)/86400000 == 1){
              end = start.slice(0,11)+'23:59';
            }
          } else if(end.includes('TZID=Asia/Bangkok')){
            end = end.split(':')[1];
            end = end.slice(4,6)+'-'+end.slice(6,8)+'-'+end.slice(0,4)+' '+end.slice(9,11)+':'+end.slice(11,13);
            let startdate = new Date(start);
            let enddate = new Date(end);
            let startdatetime = startdate.getTime();
            let enddatetime = enddate.getTime();
            if((enddatetime-startdatetime)/86400000 == 1){
              end = start.slice(0,11)+'23:59';
            }
          }
        }
        if(event[j].includes('SUMMARY')){
          summary = event[j].split(':')[1];
        }
      }
      // levents.push([start,end,summary,'goingon']);
      if(location == undefined){
        location = '';
      }
      levents.push([start,end,location,summary,'goingon']);
    }
    console.log(levents)
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
      levents[i][6] = 'https://cdn-icons-png.flaticon.com/512/5973/5973800.png'
      if(levents[i][2].trim() == 'กรุงเทพ'){
        levents[i][6] = 'https://img.gs/fhcphvsghs/120x120,crop/https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Seal_of_Bangkok_Metro_Authority.png/2048px-Seal_of_Bangkok_Metro_Authority.png'
      }
      if(levents[i][2].trim() == 'ภูเก็ต'){
        levents[i][6] = 'https://img.gs/fhcphvsghs/120x120,crop/https://www.phuket.go.th/webpk/images/introduce/logo-phuket2565.jpg'
      }
      if(levents[i][2].trim() == 'นนทบุรี' || levents[i][3].includes('บริษัท')){
        levents[i][6] = 'https://gdcatalog.go.th/assets/images/76province/NBI.png'
      }
      if(levents[i][2].trim() == 'ขอนแก่น'){
        levents[i][6] = 'https://img.gs/fhcphvsghs/120x120,crop/https://khonkaen.m-culture.go.th/web-upload/1005x9680e19a89465bf0531f017d8ef94780/tinymce/94-bfc6edecc2a4da646bd0824086ba8dea/%E0%B8%AA%E0%B8%B1%E0%B8%8D%E0%B8%A5%E0%B8%B1%E0%B8%81%E0%B8%A9%E0%B8%93%E0%B9%8C%E0%B8%9B%E0%B8%A3%E0%B8%B0%E0%B8%88%E0%B8%B3%E0%B8%88%E0%B8%B1%E0%B8%87%E0%B8%AB%E0%B8%A7%E0%B8%B1%E0%B8%94/khonkaenLogo.png'
      }
      if(levents[i][2].trim() == 'พัทยา' || levents[i][3].includes('พัทยา')){
        levents[i][6] = 'https://upload.wikimedia.org/wikipedia/commons/6/64/Pattaya_seal.png'
      }
      console.log(nowtime)
      console.log(endtime)
      if((nowtime<=starttime || nowtime<=endtime) && levents[i][4] == 'goingon'){
        eventlist.push(levents[i]);
      }
    }
    //order by eventlist[0] start time in coming will be first
    eventlist.sort(function(a,b){
      let starta = new Date(a[0]);
      let startb = new Date(b[0]);
      let startatime = starta.getTime();
      let startbtime = startb.getTime();
      return startatime - startbtime;
    })
    return eventlist;
  }
  async function getoldevents(levents){
    let now = new Date();
    let nowtime = now.getTime();
    let eventlist = [];
    //reoder levents by start time
    levents.sort(function(a,b){
      let starta = new Date(a[0]);
      let startb = new Date(b[0]);
      let startatime = starta.getTime();
      let startbtime = startb.getTime();
      return startbtime - startatime;
    })
    for(let i=0;i<levents.length;i++){
      let start = new Date(levents[i][0]);
      let end = new Date(levents[i][1]);
      let starttime = start.getTime();
      let endtime = end.getTime();
      // let response = await fetch("https://anywhere.pwisetthon.com/https://province-thai-api.vercel.app");
      // let data = await response.json();
      //get provinceName by levents[i][2]
      // for(let j=0;j<data.length;j++){
      //   if(data[j].provinceName == levents[i][3]){
      //     levents[i][6] = data[j].sealUrl;
      //     break;
      //   }
      // }
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
          <p style="display: inline-flex;"><Avatar src="https://cdn-icons-png.flaticon.com/512/5973/5973800.png" /> บ้าน</p>
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
              <AccordionItem header="{getthaiformat(event[0])} - {event[3]}">
                <!--Card body-->
                <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
                <!-- <p style="display: inline-flex;"><Avatar src={event[6]} /> {event[3]}</p> -->
                <Row class="mb-3">
                  <Col xs="auto"><Avatar src={event[6]} /></Col>
                  <Col>
                    <Row>
                      <Col xs="12">{event[2]}</Col>
                      <Col xs="12">{event[3]}</Col>
                    </Row>
                  </Col>
                </Row>
                <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
                <!--/Card-->
              </AccordionItem>
            {:else}
              <AccordionItem header="{getthaiformat(event[0])} - {event[3]}">
                <!--Card body-->
                <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
                <!-- <p style="display: inline-flex;"><Avatar src={event[6]} /> {event[3]}</p> -->
                <Row>
                  <Col xs="auto"><Avatar src={event[6]} /></Col>
                  <Col class="mb-3">
                    <Row>
                      <Col xs="12">{event[2]}</Col>
                      <Col xs="12">{event[3]}</Col>
                    </Row>
                  </Col>
                </Row>
                <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
                <!--/Card-->
              </AccordionItem>
            {/if}
          {/each}
        {:catch error}
          <Card body><p class="mb-0">Error...... F5 For Refresh {error}</p></Card>
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
                <!-- <p style="display: inline-flex;"><Avatar src={event[6]} /> {event[3]}</p> -->
                <Row>
                  <Col xs="auto"><Avatar src={event[6]} /></Col>
                  <Col class="mb-3">
                    <Row>
                      <Col xs="12">{event[2]}</Col>
                      <Col xs="12">{event[3]}</Col>
                    </Row>
                  </Col>
                </Row>
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
