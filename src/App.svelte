<head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css">
</head>

<script>
  let headtitle = "";
  import { Button,Styles,Container,Row,Col,Card,CardBody,Icon } from 'sveltestrap/src';
  if(window.location.href == 'https://bussy.pwisetthon.com'){
    headtitle = "พงศกร วิเศษธร (บอย)"
  } else if(window.location.href == 'https://bussy.teamquadb.in.th'){
    headtitle = "พงศกร วิเศษธร (บอย)"
  }
  console.log(window.location.href)
</script>

<main>
  <Container sm>
    <Row>
      <Col sm="12" md={{ size: 6, offset: 3 }}>
        <Card body><center><h2>ตารางงานของ {headtitle}</h2></center></Card>
        <Card body color="info" class="mb-3"><Icon name="info-square-fill" /> ยังไม่มีตารางงานของ {headtitle}</Card>
      </Col>
    </Row>
  </Container>
  <!--Button color="primary">Hello World!</Button-->
</main>

<style>
  main {
    background-color: darkgray;
    min-height: 100%;
  }
</style>
