/**
 * bootloader: v0.0.1
 */
BTLDR.svg.setAttribute("viewBox","0 0 400 400");
const W=400,H=400,cx=W/2,cy=H/2;

// --- helpers ---
function makeEl(tag,attrs={},kids=[]){
  const el=document.createElementNS("http://www.w3.org/2000/svg",tag);
  for(let k in attrs)el.setAttribute(k,attrs[k]);
  kids.forEach(k=>el.appendChild(k));
  return el;
}
function pick(arr){return arr[Math.floor(BTLDR.rnd()*arr.length)];}

// --- traits ---
const eyeStyle=Math.floor(BTLDR.rnd()*4);
const noseStyle=Math.floor(BTLDR.rnd()*3);
const mouthStyle=Math.floor(BTLDR.rnd()*3);
const palette=Math.floor(BTLDR.rnd()*4);

const palettes=[
  {bg:"#000",stroke:"#fff",accent:"#ccc"},
  {bg:"#0a0a0a",stroke:"#0ff",accent:"#f0f"},
  {bg:"#fdf6e3",stroke:"#dc322f",accent:"#b58900"},
  {bg:"#111122",stroke:"#39cccc",accent:"#7fdbff"}
];
const pal=palettes[palette];

// --- background ---
BTLDR.svg.appendChild(makeEl("rect",{x:0,y:0,width:W,height:H,fill:pal.bg}));

// --- eyes (with pupil) ---
function drawEyes(style){
  const g=makeEl("g",{});const ex1=cx-80,ex2=cx+80,ey=cy-50;
  [ex1,ex2].forEach(ex=>{
    // style variations
    if(style===0){ // vinyl rings
      for(let i=0;i<5;i++){
        const r=10+i*8;
        const c=makeEl("circle",{cx:ex,cy:ey,r,stroke:pal.stroke,"stroke-width":1,fill:"none"});
        c.appendChild(makeEl("animate",{attributeName:"r",values:`${r};${r*1.2};${r}`,dur:`${3+BTLDR.rnd()*2}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()*2}s`}));
        g.appendChild(c);
      }
    }
    if(style===1){ // bold rotating ring
      const ring=makeEl("circle",{cx:ex,cy:ey,r:30,stroke:pal.accent,"stroke-width":6,fill:"none"});
      ring.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",from:`0 ${ex} ${ey}`,to:`360 ${ex} ${ey}`,dur:`${5+BTLDR.rnd()*3}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()}s`}));
      g.appendChild(ring);
    }
    if(style===2){ // radial spokes
      for(let i=0;i<12;i++){
        const a=i*(Math.PI/6),x2=ex+Math.cos(a)*25,y2=ey+Math.sin(a)*25;
        const l=makeEl("line",{x1:ex,y1:ey,x2,y2,stroke:pal.stroke,"stroke-width":2});
        l.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",from:`0 ${ex} ${ey}`,to:`360 ${ex} ${ey}`,dur:`${6+BTLDR.rnd()*2}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()}s`}));
        g.appendChild(l);
      }
    }
    if(style===3){ // spiky polygon
      let pts="";for(let i=0;i<12;i++){const r=20+(i%2)*10,a=i*(Math.PI/6);pts+=`${ex+Math.cos(a)*r},${ey+Math.sin(a)*r} `;}
      const poly=makeEl("polygon",{points:pts,fill:"none",stroke:pal.accent,"stroke-width":2});
      poly.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",from:`0 ${ex} ${ey}`,to:`360 ${ex} ${ey}`,dur:`${7+BTLDR.rnd()*3}s`,repeatCount:"indefinite"}));
      g.appendChild(poly);
    }

    // central pupil
    const pupilR = 4 + BTLDR.rnd()*4;
    const pupil = makeEl("circle",{cx:ex,cy:ey,r:pupilR,fill:pal.stroke,stroke:pal.bg,"stroke-width":1.5});
    const dx = (BTLDR.rnd()-0.5)*10;
    const dy = (BTLDR.rnd()-0.5)*10;
    const values = `0 0; ${dx} ${dy}; ${-dx} ${dy}; 0 0`;
    const dur = (2+BTLDR.rnd()*3).toFixed(1)+"s";
    pupil.appendChild(makeEl("animateTransform",{
      attributeName:"transform",type:"translate",
      values, dur, repeatCount:"indefinite",
      begin:`${BTLDR.rnd()*2}s`
    }));
    g.appendChild(pupil);
  });
  BTLDR.svg.appendChild(g);
}
drawEyes(eyeStyle);

// --- nose ---
function drawNose(style){
  const g=makeEl("g",{});
  if(style===0){
    const nose=makeEl("polygon",{points:`${cx},${cy-20} ${cx-20},${cy+40} ${cx+20},${cy+40}`,fill:pal.accent});
    nose.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",values:`-10 ${cx} ${cy};10 ${cx} ${cy};-10 ${cx} ${cy}`,dur:`${3+BTLDR.rnd()*2}s`,repeatCount:"indefinite"}));
    g.appendChild(nose);
  }
  if(style===1){
    const diamond=makeEl("polygon",{points:`${cx},${cy-30} ${cx-20},${cy} ${cx},${cy+30} ${cx+20},${cy}`,fill:pal.stroke});
    diamond.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",values:`-5 ${cx} ${cy};5 ${cx} ${cy};-5 ${cx} ${cy}`,dur:`${4+BTLDR.rnd()*2}s`,repeatCount:"indefinite"}));
    g.appendChild(diamond);
  }
  if(style===2){
    const line=makeEl("line",{x1:cx,y1:cy-20,x2:cx,y2:cy+40,stroke:pal.stroke,"stroke-width":4});
    line.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"rotate",values:`-15 ${cx} ${cy};15 ${cx} ${cy};-15 ${cx} ${cy}`,dur:`${2+BTLDR.rnd()*2}s`,repeatCount:"indefinite"}));
    g.appendChild(line);
  }
  BTLDR.svg.appendChild(g);
}
drawNose(noseStyle);

// --- mouth ---
function drawMouth(style){
  const g=makeEl("g",{});const y=cy+80;
  if(style===0){ // piano
    for(let i=0;i<12;i++){
      const x=cx-60+i*10;
      const key=makeEl("rect",{x,y,width:8,height:30,fill:(i%2?pal.stroke:pal.accent)});
      key.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"translate",values:`0,0;0,5;0,0`,dur:`${1+BTLDR.rnd()*1.5}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()*2}s`}));
      g.appendChild(key);
    }
  }
  if(style===1){ // broken cluster
    for(let i=0;i<8;i++){
      const x=cx-50+i*12,h=20+BTLDR.rnd()*20;
      const k=makeEl("rect",{x,y,width:10,height:h,fill:pal.accent});
      k.appendChild(makeEl("animateTransform",{attributeName:"transform",type:"translate",values:`0,0;0,6;0,0`,dur:`${1+BTLDR.rnd()}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()*1.5}s`}));
      g.appendChild(k);
    }
  }
  if(style===2){ // neon bars
    for(let i=0;i<6;i++){
      const x=cx-45+i*15;
      const bar=makeEl("rect",{x,y,width:12,height:25,fill:"none",stroke:pal.accent,"stroke-width":3});
      bar.appendChild(makeEl("animate",{attributeName:"y",values:`${y};${y+5};${y}`,dur:`${1+BTLDR.rnd()}s`,repeatCount:"indefinite",begin:`${BTLDR.rnd()*2}s`}));
      g.appendChild(bar);
    }
  }
  BTLDR.svg.appendChild(g);
}
drawMouth(mouthStyle);
