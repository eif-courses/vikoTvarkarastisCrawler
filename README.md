# vikoTvarkarastisCrawler
Viko tvarkaraščio crawleris skirtas ištraukti dėstytojų informaciją.

const rp = require('request-promise');
const url = 'https://vikoeif.edupage.org/timetable/';

rp(url)
    .then(function(html){
        //success!

        // https://regex101.com/
        let matched = html.match(/{"table":"teachers",[\w\W]*?\(-a\)"}]}/gm);
        for(let k in matched[0]) {

            console.log(JSON.parse(matched[0]).rows[k].short,
                JSON.parse(matched[0]).rows[k].id,
                "https://vikoeif.edupage.org/timetable/view.php?teacher="+JSON.parse(matched[0]).rows[k].id.toString()+"");
        }

    })
    .catch(function(err){
        //handle error
    });
