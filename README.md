'use strict';

const fs = require('fs');

process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', inputStdin => {
    inputString += inputStdin;
});

process.stdin.on('end', _ => {
    inputString = inputString.trim().split('\n').map(str => str.trim());

    main();
});

function readLine() {
    return inputString[currentLine++];
}

/*
 * Complete the timeConversion function below.
 */

function timeConversion(s) {
    
    var s = [...s];
    if (s[8] == "P"&& !(s[0]== 1 && s[1] == 2)) {
        s[1] = parseInt(s[0]+s[1])+ 12 ;
        s = s.slice(1,8);
    } else if ( (s[8] == "P") && (s[0]== 0 && s[1] == 0)){
        s[1] = parseInt(s[1])+ 12 ;
        s = s.slice(1,8);
    }else if ( s[8] == "A" && (s[0]== 1 && s[1] == 2)){
        s[0] = 0 ;
        s[1] = 0 ;
        s = s.slice(0,8);
    }else { 
        s = s.slice(0,8)
    }
   
   
    s = s.join('') ;
    return s;
}


function main() {
    const ws = fs.createWriteStream(process.env.OUTPUT_PATH);

    const s = readLine();

    let result = timeConversion(s);

    ws.write(result + "\n");

    ws.end();
}
