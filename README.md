# [Morse Code Translator](https://morsecodetranslator.cc)

[![npm-version]][npm] [![npm-downloads]][npm]

[Morse code encoder](https://morsecodetranslator.cc) and [Morse code decoder](https://morsecodetranslator.cc) with no dependencies. It supports Latin, Cyrillic, Greek, Hebrew, Arabic,
Persian, Japanese, Korean, and Thai, with audio-generation functionality using the [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API).

## Installation

### npm

```bash
$ npm install @ozdemirburak/morse-code-translator --save
```

## Usage

```js
import morse from '@ozdemirburak/morse-code-translator';

const encoded = morse.encode('SOS'); // ... --- ...
const decoded = morse.decode('... --- ...'); // SOS
const characters = morse.characters(); // {'1': {'A': '.-', ...}, ..., '11': {'ㄱ': '.-..', ...}}

const audio = morse.audio('SOS');
audio.play(); // play audio
audio.stop(); // stop audio (cannot resume)
audio.exportWave(); // download audio wave file (promise)
const url = await audio.getWaveUrl(); // get audio wave url (promise)
const blob = await audio.getWaveBlob(); // get audio wave blob (promise)
```

### Options and localization

You can customize the dash, dot, or space characters and specify the alphabet with the priority option for
an accurate encoding and decoding.

The priority option gives direction to the plugin to start searching for the given character set first.

Set the priority option according to the list below.

- 1 => ASCII (Default)
- 2 => Numbers
- 3 => Punctuation
- 4 => Latin Extended (Turkish, Polish etc.)
- 5 => Cyrillic
- 6 => Greek
- 7 => Hebrew
- 8 => Arabic
- 9 => Persian
- 10 => Japanese
- 11 => Korean
- 12 => Thai

```js
const cyrillic = morse.encode('Ленинград', { priority: 5 }); // .-.. . -. .. -. --. .-. .- -..
const greek = morse.decode('... .- --. .- .--. .--', { priority: 6 }); // ΣΑΓΑΠΩ
const hebrew = morse.decode('.. ––– . –––', { dash: '–', dot: '.', priority: 7 }); // יהוה
const japanese = morse.encode('NEWS', { priority: 10, dash: '－', dot: '・', separator: '　' }); // －・　・　・－－　・・・
const characters = morse.characters({ dash: '–', dot: '•' }); // {'1': {'A': '•–', ...}, ..., '11': {'ㄱ': '•–••', ...}}
const arabicAudio = morse.audio('البراق', { // generates the Morse .- .-.. -... .-. .- --.- then generates the audio from it
  wpm: 18, // sets the wpm based on the Paris method, note that setting this will override and set the unit and fwUnits accordingly
  unit: 0.1, // period of one unit, in seconds, 1.2 / c where c is speed of transmission, in words per minute
  fwUnit: 0.1, // period of one Farnsworth unit to control intercharacter and interword gaps
  volume: 100, // the volume in percent (0-100)
  oscillator: {
    type: 'sine', // sine, square, sawtooth, triangle
    frequency: 500,  // value in hertz
    onended: function () { // event that fires when the tone stops playing
      console.log('ended');
    }
  }
});
const oscillator = arabicAudio.oscillator; // OscillatorNode
const context = arabicAudio.context; // AudioContext;
const gainNode = arabicAudio.gainNode; // GainNode
arabicAudio.play(); // will start playing Morse audio
arabicAudio.stop(); // will stop playing Morse audio
```

## Contributions

[morse-code-translator](https://github.com/ozdemirburak/morse-code-translator) has been developed 
with extensive feedback and contributions from [numerous developers](https://github.com/ozdemirburak/morse-code-translator/graphs/contributors).

Special thanks to [Chris Jones](https://github.com/chris--jones), who added many great features.

## References

Please consider referencing the website of this project, if you find this package useful for your work.

```html
<a href="https://morsecodetranslator.cc">Morse Code Translator</a>
```

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.

  [npm-version]: https://img.shields.io/npm/v/@ozdemirburak/morse-code-translator.svg?style=flat-square
  [npm-downloads]: https://img.shields.io/npm/dm/@ozdemirburak/morse-code-translator.svg?style=flat-square
  [npm]: https://www.npmjs.com/package/@ozdemirburak/morse-code-translator
