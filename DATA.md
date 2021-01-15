# Clue data

Use this data to model your game cards into objects.

### Suspects

mrGreen <br>
firstName: Jacob <br>
lastName: Green<br>
occupation: Entrepreneur<br>
age: 45 <br>
description: He has a lot of connections<br>
image: https://pbs.twimg.com/profile_images/506787499331428352/65jTv2uC.jpeg <br>
color: green <br>

drOrchid<br>
firstName: Doctor<br>
lastName: Orchid<br>
occupation: Scientist<br>
age: 26<br>
description: PhD in plant toxicology. Adopted daughter of Mr. Boddy<br>
image: http://www.radiotimes.com/uploads/images/Original/111967.jpg<br>
color: white<br>

profPlum<br>
firstName: Victor<br>
lastName: Plum<br>
occupation: Designer<br>
age: 22<br>
description: Billionaire video game designer<br>
image: https://66.media.tumblr.com/ee7155882178f73b3781603f0908617c/tumblr_phhxc7EhPJ1w5fh03_540.jpg <br>
color: purple<br>

missScarlet<br>
firstName: Kasandra<br>
lastName: Scarlet<br>
occupation: Actor<br>
age: 31<br>
description: She is an A-list movie star with a dark past<br>
image: https://www.radiotimes.com/uploads/images/Original/111967.jpg<br>
color: red<br>

mrsPeacock<br>
firstName: Eleanor<br>
lastName: Peacock<br>
occupation: Socialité<br>
age: 36<br>
description: She is from a wealthy family and uses her status and money to earn popularity<br>
image: https://metrouk2.files.wordpress.com/2016/07/mrs-peacock.jpg<br>
color: blue<br>

mrMustard<br>
firstName: Jack<br>
lastName: Mustard<br>
occupation: Retired Football player<br>
age: 62<br>
description: He is a former football player who tries to get by on his former glory<br>
image: https://static.independent.co.uk/s3fs-public/thumbnails/image/2016/07/04/08/unspecified-3.jpg<br>
color: yellow<br>

### Weapons

name: rope --- weight: 10<br>
name: knife --- weight: 8<br>
name: candlestick --- weight: 2<br>
name: dumbbell --- weight: 30<br>
name: poison --- weight: 2<br>
name: axe --- weight: 15<br>
name: bat --- weight: 13<br>
name: trophy --- weight: 25<br>
name: pistol --- weight: 20<br>

### Rooms

name: Dining Room<br>
name: Conservatory<br>
name: Kitchen<br>
name: Study<br>
name: Library<br>
name: Billiard Room<br>
name: Lounge<br>
name: Ballroom<br>
name: Hall<br>
name: Spa<br>
name: Living Room<br>
name: Observatory<br>
name: Theater<br>
name: Guest House<br>
name: Patio<br>

Find a random element of the array - selectRandom', () => {
  it('should define selectRandom', () => {
    expect(typeof selectRandom).toBe('function');
  });

  it('should return undefined if the array is empty', () => {
    expect(selectRandom([])).toBe(undefined);
  });

  it('should return the element of a single value array', () => {
    expect(selectRandom(['ab'])).toBe('ab');
  });

  it('should return an element of the array', () => {
    const array = ['ab', 'zz', 'zx', 'zy'];
    expect(array.indexOf(selectRandom(array))).toBeGreaterThan(-1);
  });

  it('should return a random element of the array', () => {
    const spy = spyOn(Math, 'random');

    spy.and.returnValue(0.5);
    expect(selectRandom(['a', 'ab', 'abb', 'aab', 'aaa', 'sda', 'kas'])).toEqual('aab');

    spy.and.returnValue(0.1);
    expect(selectRandom(['a', 'ab', 'abb', 'aab', 'aaa', 'sda', 'kas'])).toEqual('a');

    spy.and.returnValue(0.9);
    expect(selectRandom(['a', 'ab', 'abb', 'aab', 'aaa', 'sda', 'kas'])).toEqual('kas');
  });
});

describe('Pick a random mystery - pickMystery', () => {
  it('should define pickMystery', () => {
    expect(typeof pickMystery).toBe('function');
  });

  it('should return an object', () => {
    expect(Object.prototype.toString.call(pickMystery())).toEqual('[object Object]');
  });

  it('should return an object with 3 properties', () => {
    expect(Object.keys(pickMystery()).length).toEqual(3);
  });

  it('should return a suspect in the suspect property of the object', () => {
    let suspect = JSON.stringify(pickMystery().suspect);
    expect(suspectsArray.findIndex(el => JSON.stringify(el) === suspect)).toBeGreaterThan(-1);
  });

  it('should return a weapon in the weapon property of the object', () => {
    let weapon = JSON.stringify(pickMystery().weapon);
    expect(weaponsArray.findIndex(el => JSON.stringify(el) === weapon)).toBeGreaterThan(-1);
  });

  it('should return a room in the room property of the object', () => {
    let room = JSON.stringify(pickMystery().room);
    expect(roomsArray.findIndex(el => JSON.stringify(el) === room)).toBeGreaterThan(-1);
  });
});

describe('Reveal the mystery - revealMystery', () => {
  it('should define revealMystery', () => {
    expect(typeof revealMystery).toBe('function');
  });

  it('should return a string', () => {
    expect(
      typeof revealMystery({
        suspect: { firstName: 'aa', lastName: 'abc' },
        weapon: { name: 'abd' },
        room: { name: 'abb' }
      })
    ).toEqual('string');
  });

  it('should return "<FIRST NAME> <LAST NAME> killed Mr. Boddy using the <WEAPON> in the <PLACE>!"', () => {
    expect(
      revealMystery({
        suspect: { firstName: 'Victor', lastName: 'Plum' },
        weapon: { name: 'poison' },
        room: { name: 'Billiard Room' }
      })
    ).toEqual('Victor Plum killed Mr. Boddy using the poison in the Billiard Room!');
  });
});