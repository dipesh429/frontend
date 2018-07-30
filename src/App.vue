<template>
  <v-app>
    <v-navigation-drawer
      fixed
      
      v-model="drawer"
      app
    >
    </v-navigation-drawer>
    <v-toolbar fixed app >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <b>FOOTBALL PREDICTION</b>
    </v-toolbar>
    <v-content>
      <v-container fluid>

      <h2>Parameters</h2>


<br>

       
      <v-layout row wrap>
      <v-flex  sm6> 

      <v-layout row wrap>
      <v-flex xs5 sm6>
        <v-subheader v-text="'Home Team'"></v-subheader>
      </v-flex>
      <v-flex xs6  sm6>
        <v-select

          :items="club"
          v-model="a1"
          label="Select Home Team"
          autocomplete
        ></v-select>
      </v-flex>
    </v-layout>

      <v-layout>
      <v-flex xs5 sm6>
        <v-subheader v-text="'Away Team'"></v-subheader>
      </v-flex>
      <v-flex xs6 sm6>
        <v-select
          :items="club"
          v-model="a2"
          label="Select Away Team"
          autocomplete
        ></v-select>
      </v-flex>
    </v-layout>
   

</v-flex>

<v-flex xs5 offset-xs1 sm5 offset-sm1>

  <v-progress-circular :size="50" indeterminate color="primary" v-if="ok" ></v-progress-circular>

  <app-chart :chart-data="datas" :width="300" :height="200" v-if=" dataprep.length!=0"> </app-chart>


</v-flex> 

</v-layout>

  <v-btn color="success" @click="send" >Predict</v-btn>



<br>
<br>

<br>
<br>




<v-layout>
<v-flex sm10 offset-sm1>  
  
 <v-stepper v-model="e13" vertical v-if="start">


  <v-layout>
  <v-flex xs5 sm5>

    <v-stepper-step step="1" complete>
      {{a1}} <br>
     <span class="grey--text lighten-1">Coach: {{coach1}}</span> 
    </v-stepper-step>
    <v-stepper-content step="1">


    <!-- <v-card color="grey lighten-1" class="mb-5" height="200px"> -->
    <v-expansion-panel expand>

    <v-layout>

       <v-flex xs3 sm3 >
    <v-expansion-panel-content value=true>

      
        <div slot="header">RECENT FORM</div>
      
        <v-card  class="mb-5" height="200px">
            
          
           
          <div class="text-xs-center">
          <v-chip :class="five_match1[0][0]=='W' ? 'light-green accent-3' : five_match1[0][0]=='D' ? 'yellow lighten-1' : 'red'"> {{five_match1[0][0]}} </v-chip>
          <v-chip :class="five_match1[0][1]=='W' ? 'light-green accent-3' : five_match1[0][1]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match1[0][1]}} </v-chip> 
          <v-chip :class="five_match1[0][2]=='W' ? 'light-green accent-3' : five_match1[0][2]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match1[0][2]}} </v-chip> 
          <v-chip :class="five_match1[0][3]=='W' ? 'light-green accent-3' : five_match1[0][3]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match1[0][3]}} </v-chip> 
          <v-chip :class="five_match1[0][4]=='W' ? 'light-green accent-3' : five_match1[0][4]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match1[0][4]}} </v-chip> 
          </div>
         
          
    
          
        </v-card>
    </v-expansion-panel-content>
    </v-flex> 

    <v-flex xs4 offset-xs2 sm4 offset-sm2 >
    <v-expansion-panel-content value=true>

      
        <div slot="header">LAST SEASON</div>
      
        <v-card  class="mb-5" height="200px">
            
          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{total_game1}}</v-avatar>
            TOTAL GAME  
          </v-chip> 
          </div>
          
          <div class="text-xs-left">
          <v-chip>
          <v-avatar class="teal">{{win1}}</v-avatar>
            WIN
          </v-chip>     
          </div>

          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{draw1}}</v-avatar>
            DRAW
          </v-chip> 
          </div>

          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{loss1}}</v-avatar>
            LOSS
          </v-chip> 
          </div>


          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{points1}}</v-avatar>
            TOTAL POINTS
          </v-chip> 
          </div>
          
          
    
          
        </v-card>
    </v-expansion-panel-content>
    </v-flex> 
    </v-layout>
    
  </v-expansion-panel>
<!-- </v-card> -->

      
      <!-- <v-btn color="primary" @click.native="e13 = 2">Continue</v-btn> -->
      <!-- <v-btn flat>Cancel</v-btn> -->
    </v-stepper-content>

  </v-flex>

    

    <v-flex xs5 offset-xs1 sm5 offset-sm1>
    <v-stepper-step step="1" complete>{{a2}} <br>
     <span class="grey--text lighten-1">Coach: {{coach2}}</span> </v-stepper-step>
    <v-stepper-content step="1">
      
    <v-expansion-panel expand>
    
    <v-layout>

    <v-flex xs3 sm3>
    
    <v-expansion-panel-content value=true>

      
        <div slot="header">RECENT FORM</div>
      
        <v-card  class="mb-5" height="200px">
            
          
           
          <div class="text-xs-center">
          <v-chip :class="five_match2[0][0]=='W' ? 'light-green accent-3' : five_match2[0][0]=='D' ? 'yellow lighten-1' : 'red'"> {{five_match2[0][0]}} </v-chip>
          <v-chip :class="five_match2[0][1]=='W' ? 'light-green accent-3' : five_match2[0][1]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match2[0][1]}} </v-chip> 
          <v-chip :class="five_match2[0][2]=='W' ? 'light-green accent-3' : five_match2[0][2]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match2[0][2]}} </v-chip> 
          <v-chip :class="five_match2[0][3]=='W' ? 'light-green accent-3' : five_match2[0][3]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match2[0][3]}} </v-chip> 
          <v-chip :class="five_match2[0][4]=='W' ? 'light-green accent-3' : five_match2[0][4]=='D' ? 'yellow lighten-1' : 'red lighten-1'"> {{five_match2[0][4]}} </v-chip> 
          </div>
         
          
    
          
        </v-card>
    </v-expansion-panel-content>
    </v-flex> 

     <v-flex sm4 offset-sm2 xs4 offset-xs2 >
    <v-expansion-panel-content value=true>

      
        <div slot="header">LAST SEASON</div>
      
        <v-card  class="mb-5" height="200px">
            
          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{total_game2}}</v-avatar>
            TOTAL GAME  
          </v-chip> 
          </div>
          
          <div class="text-xs-left">
          <v-chip>
          <v-avatar class="teal">{{win2}}</v-avatar>
            WIN
          </v-chip>     
          </div>

          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{draw2}}</v-avatar>
            DRAW
          </v-chip> 
          </div>

          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{loss2}}</v-avatar>
            LOSS
          </v-chip> 
          </div>


          <div class="text-xs-left">  
          <v-chip>
          <v-avatar class="teal">{{points2}}</v-avatar>
            TOTAL POINTS
          </v-chip> 
          </div>
          
          
    
          
        </v-card>
    </v-expansion-panel-content>
    </v-flex> 
    </v-layout>
    
  </v-expansion-panel>
  
    </v-stepper-content>
  </v-flex>
  </v-layout>  

  </v-stepper>
</v-flex>
</v-layout>
 
</v-container>
         
     
    </v-content>
    
    <v-footer :fixed="fixed" app>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>

  import Chart from './chart.vue'

  export default {

    components: {

      'app-chart':Chart},

    data () {
      return {
        datas:null,
        dataprep:[],
        total_game1:0,
        win1:0,
        loss1:0,
        draw1:0,
        points1:0,
        coach1:'',
        coach2:'',
        five_match1:[],
        total_game2:0,
        win2:0,
        loss2:0,
        draw2:0,
        points2:0,
        five_match2:[],
        a1:null,
        ok:false,
        start:false,
        a2:null,
        e13:1,
        drawer: false,
        fixed: false,
        club: ["MANCHESTER CITY", "MANCHESTER UNITED", "TOTTENHAM HOTSPUR", "LIVERPOOL","CHELSEA","ARSENAL","BURNLEY","EVERTON","LEICESTER CITY","NEWCASTLE UNITED", "CRYSTAL PALACE", "AFC BOURNEMOUTH","WEST HAM UNITED","WATFORD","BRIGHTON & HOVE ALBION",  "HUDDERSFIELD TOWN","SOUTHAMPTON", "SWANSEA CITY", "STOKE CITY","WEST BROMWICH ALBIONWEST"],
        form:{
            coach:['Pep Guardiola','José Mourinho','Mauricio Pochettino','Jürgen Klopp','Antonio Conte', 'Unai Emery', 'Sean Dyche', 'Marco Silva', 'Claude Puel', 'Rafael Benítez','Roy Hodgson','Eddie Howe', 'Manuel Pellegrini', 'Javi Gracia', 'Chris Hughton', 'David Wagner', 'Mark Hughes', 'Carlos Carvalhal', 'Paul Lambert', 'Darren Moore'],
            total_game:[38,38,38,38,38,38,38,38,38,38,38,38,38,38,38,38,38,38,38,38],
            win:[32,25,23,21,21,19,14,13,12,12,11,11,10,11,9,9,7,8,7,6],
            draw:[4,6,8,12,7,6,12,10,11,8,11,11,12,8,13,10,15,9,12,13],
            loss:[2,7,7,5,10,13,12,15,15,18,16,16,16,19,16,19,16,21,19,19],
            point:[100,81,77,75,70,63,54,49,47,44,44,44,42,41,40,37,36,33,33,31],
            five_match:[['W','W','D','W','W'],
                        ['W','D','L','W','W'],
                        ['W','W','L','W','D'],
                        ['W','L','D','D','W'],
                        ['L','D','W','W','W'],
                        ['W','L','W','L','W'],
                        ['L','L','D','D','L'],
                        ['L','D','W','W','D'],
                        ['L','W','L','L','D'],
                        ['W','L','L','L','L'],
                        ['W','W','W','D','W'],
                        ['W','W','L','L','L'],
                        ['W','D','W','L','L'],
                        ['L','W','L','D','L'],
                        ['L','L','W','D','D'],
                        ['L','D','D','L','W'],
                        ['L','W','D','W','D'],
                        ['L','L','L','L','L'],
                        ['W','L','D','D','D'],
                        ['L','W','W','D','W']]      
    }}},

    methods:{


      send(){

        this.ok=true
        this.start=true


        var index1=this.club.indexOf(this.a1)
        var index2=this.club.indexOf(this.a2)
        

        this.total_game1=this.form.total_game[index1]
        this.win1=this.form.win[index1]
        this.draw1=this.form.draw[index1]
        this.loss1=this.form.loss[index1]
        this.points1=this.form.point[index1]
        this.five_match1.push(this.form.five_match[index1])
        this.coach1=this.form.coach[index1]

        
        this.total_game2=this.form.total_game[index2]
        this.win2=this.form.win[index2]
        this.draw2=this.form.draw[index2]
        this.loss2=this.form.loss[index2]
        this.points2=this.form.point[index2]
        this.five_match2.push(this.form.five_match[index2])
        this.coach2=this.form.coach[index2]


       
        var count1=0
        var count2=0

        this.five_match1[0].forEach((each)=>{

                    if(each=='W'){
                        count1+=1
                    }

                    if(each=='D'){
                        count1+=0.5
                    }  
        })


        this.five_match2[0].forEach((each)=>{

                    if(each=='W'){
                        count2+=1
                    }

                    if(each=='D'){
                        count2+=0.5
                    }  
        })

        

        var data={

            home: this.a1,
            away: this.a2,
            count1: count1/5,
            count2: count2/5

        }

        fetch('https://flaskminor.herokuapp.com/parameters',{

          method:'POST',
          headers:{
            'Content-Type':'application/json'
          },
          body: JSON.stringify(data)
        }).then((res)=> {
            return res.json()})
          .then((ress)=>{
            console.log(ress)




              this.dataprep=[]
              this.ok=false
             
              this.dataprep.push(ress.a*100)
              this.dataprep.push(ress.b*100)
              this.dataprep.push(ress.c*100)
              
              
              this.datas={


                    labels: ['Win', 'Draw','Loss'],
                    datasets: [
                      {
                        label: 'GitHub Commits',
                        backgroundColor: ['red','purple','blue'],
                        data: this.dataprep
                      },

  ]
    } 


            
           
          })
      }
    }
  }
</script>



// WEBPACK FOOTER //
// src/App.vue
