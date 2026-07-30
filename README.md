// Improved win detection: check rows, columns, diagonals and highlight winning cells
function checkWin(data){
  // data expected as array of 9 strings (row-major order)
  const lines = [
    [0,1,2],[3,4,5],[6,7,8], // rows
    [0,3,6],[1,4,7],[2,5,8], // cols
    [0,4,8],[2,4,6]          // diagonals
  ];
  const winners = new Set();
  lines.forEach(([a,b,c])=>{
    if(data[a] && data[a]===data[b] && data[b]===data[c]){
      winners.add(a); winners.add(b); winners.add(c);
    }
  });

  // apply/remove win class per cell
  cells.forEach((cell, idx)=>{
    if(winners.has(idx)) cell.classList.add('win');
    else cell.classList.remove('win');
  });

  if(winners.size > 0){
    result.textContent='🎉 恭喜中獎！';
    playAudioElementOrFallback(winAudioElem, playWinMelody);
  } else {
    result.textContent='😆 再接再厲！';
  }
}
