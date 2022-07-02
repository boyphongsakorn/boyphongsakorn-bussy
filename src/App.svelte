<script>
  import { Styles,Card,Row,Col,Icon } from 'sveltestrap';
  let name = ''
  if(window.location.hostname.includes('pwisetthon')){
    name = 'พงศกร วิเศษธร (บอย)';
  }else{
    name = 'บริษัท ทีมควอดบี จำกัด';
  }
  console.log(window.location.hostname)
  let events = [['08-01-2022 00:00','08-01-2022 23:59','นนทุบรี']]
  function getoutoldevents(levents){
    let now = new Date();
    let nowtime = now.getTime();
    let eventlist = [];
    for(let i=0;i<levents.length;i++){
      let start = new Date(levents[i][0]);
      let end = new Date(levents[i][1]);
      let starttime = start.getTime();
      let endtime = end.getTime();
      if(nowtime<=starttime || nowtime<=endtime){
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

<main>
  <Row>
    <Col sm="12" md={{ size: 4, offset: 4 }}>
      <Card class="mb-1" body><center><h2>ตารางงานของ {name}</h2></center></Card>
      <!--Card body><p class="mb-0"><Icon name="info-square-fill" /> ยังไม่มีตารางงานของ {name}</p></Card-->
      {#each getoutoldevents(events) as event}
        <Card body>
          <p><Icon name="calendar-event" /> {getthaiformat(event[0])}</p>
          <p><Icon name="shield-fill" /> {event[2]}</p>
          <p><Icon name="clock-fill" /> {gettime(event[0],event[1])}</p>
        </Card>
      {/each}
    </Col>
  </Row>
</main>

<style>
  
</style>
