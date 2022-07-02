<script>
  import { Styles,Card,Row,Col,Icon } from 'sveltestrap';
  let name = ''
  if(window.location.hostname.includes('pwisetthon')){
    name = 'พงศกร วิเศษธร (บอย)';
  }else{
    name = 'พนักงานบริษัท ทีมควอดบี จำกัด';
  }
  console.log(window.location.hostname)
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
      <Card body>
        <p><Icon name="calendar-event" /> วันที่ 1 สิงหาคม 2565</p>
        <p><Icon name="shield-fill" /> นนทุบรี</p>
        <p><Icon name="clock-fill" /> ทั้งวัน</p>
      </Card>
    </Col>
  </Row>
</main>

<style>
  
</style>
