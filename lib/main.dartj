import 'package:flutter/material.dart';

void main() => runApp(const ChatLiveApp());

const streamers = [
  ['سلمى', '12.4K', 'دردشة'],
  ['ليلى', '8.1K', 'موسيقى'],
  ['ياسمين', '5.6K', 'ألعاب'],
  ['نور', '3.2K', 'طبخ'],
  ['ريم', '2.9K', 'أسئلة'],
  ['أيوب', '1.5K', 'ألعاب'],
];

const gifts = [
  ['🌹', 'وردة', 5],
  ['❤️', 'قلب', 10],
  ['🎁', 'هدية', 30],
  ['👑', 'تاج', 100],
];

class ChatLiveApp extends StatelessWidget {
  const ChatLiveApp({super.key});
  @override
  Widget build(BuildContext context) => MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'ChatLive',
        theme: ThemeData(
            colorSchemeSeed: const Color(0xFF7C3AED), useMaterial3: true),
        builder: (c, w) =>
            Directionality(textDirection: TextDirection.rtl, child: w!),
        home: const Home(),
      );
}

class Home extends StatelessWidget {
  const Home({super.key});
  @override
  Widget build(BuildContext context) => Scaffold(
        backgroundColor: const Color(0xFFFFF4FA),
        appBar: AppBar(
          title: const Text('بث مباشر',
              style: TextStyle(fontWeight: FontWeight.w900)),
          backgroundColor: const Color(0xFFFFF4FA),
        ),
        body: GridView.builder(
          padding: const EdgeInsets.all(12),
          gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
              crossAxisCount: 2,
              mainAxisSpacing: 12,
              crossAxisSpacing: 12,
              childAspectRatio: 0.75),
          itemCount: streamers.length,
          itemBuilder: (c, i) => Tile(i: i),
        ),
      );
}

class Tile extends StatelessWidget {
  final int i;
  const Tile({super.key, required this.i});
  @override
  Widget build(BuildContext context) {
    final s = streamers[i];
    final hue = (i * 55 + 260) % 360.0;
    return InkWell(
      borderRadius: BorderRadius.circular(22),
      onTap: () => Navigator.push(
          context, MaterialPageRoute(builder: (_) => Room(i: i))),
      child: Container(
        decoration: BoxDecoration(
          borderRadius: BorderRadius.circular(22),
          gradient: LinearGradient(
            begin: Alignment.topRight,
            end: Alignment.bottomLeft,
            colors: [
              HSLColor.fromAHSL(1, hue, .7, .62).toColor(),
              HSLColor.fromAHSL(1, (hue + 40) % 360, .65, .45).toColor()
            ],
          ),
        ),
        child: Stack(children: [
          const Center(
              child: Icon(Icons.person, size: 100, color: Colors.white70)),
          Positioned(
            top: 10,
            right: 10,
            child: Container(
              padding: const EdgeInsets.symmetric(horizontal: 9, vertical: 3),
              decoration: BoxDecoration(
                  color: const Color(0xFFFF3B4E),
                  borderRadius: BorderRadius.circular(99)),
              child: const Text('مباشر',
                  style: TextStyle(
                      color: Colors.white,
                      fontSize: 12,
                      fontWeight: FontWeight.w900)),
            ),
          ),
          Positioned(
            top: 10,
            left: 10,
            child: Text('👁 ${s[1]}',
                style: const TextStyle(color: Colors.white, fontSize: 12)),
          ),
          Positioned(
            bottom: 12,
            right: 12,
            child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(s[0] as String,
                      style: const TextStyle(
                          color: Colors.white,
                          fontSize: 16,
                          fontWeight: FontWeight.bold)),
                  Text(s[2] as String,
                      style:
                          const TextStyle(color: Colors.white, fontSize: 12)),
                ]),
          ),
        ]),
      ),
    );
  }
}

class Room extends StatefulWidget {
  final int i;
  const Room({super.key, required this.i});
  @override
  State<Room> createState() => _RoomState();
}

class _RoomState extends State<Room> {
  int coins = 250;
  bool mic = false;
  int fx = 0;
  final fxs = ['بدون مؤثر', 'استوديو', 'صدى', 'قاعة كبيرة', 'صوت غنائي'];
  final msgs = <String>['مرحباً بالجميع 👋'];
  final ctl = TextEditingController();

  void say(String t) => setState(() {
        msgs.add(t);
        if (msgs.length > 30) msgs.removeAt(0);
      });

  void sendGift() {
    showModalBottomSheet(
      context: context,
      builder: (_) => Padding(
        padding: const EdgeInsets.all(16),
        child: Wrap(spacing: 12, children: [
          for (final g in gifts)
            ActionChip(
              label: Text('${g[0]} ${g[1]}  🪙${g[2]}'),
              onPressed: () {
                Navigator.pop(context);
                final price = g[2] as int;
                if (coins < price) {
                  say('رصيدك لا يكفي لهذه الهدية.');
                } else {
                  setState(() => coins -= price);
                  say('أرسلت ${g[1]} ${g[0]}');
                }
              },
            ),
        ]),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    final s = streamers[widget.i];
    return Scaffold(
      backgroundColor: const Color(0xFF1B0B33),
      appBar: AppBar(
        backgroundColor: const Color(0xFF1B0B33),
        foregroundColor: Colors.white,
        title: Text('🎤 ${s[0]}'),
        actions: [
          Center(
              child: Padding(
                  padding: const EdgeInsets.all(12),
                  child: Text('🪙 $coins')))
        ],
      ),
      body: Column(children: [
        const Expanded(
            flex: 3,
            child: Center(
                child: Icon(Icons.person, size: 160, color: Colors.white24))),
        Expanded(
          flex: 2,
          child: ListView(
            padding: const EdgeInsets.all(12),
            children: [
              for (final m in msgs)
                Align(
                  alignment: Alignment.centerRight,
                  child: Container(
                    margin: const EdgeInsets.only(bottom: 6),
                    padding: const EdgeInsets.symmetric(
                        horizontal: 12, vertical: 6),
                    decoration: BoxDecoration(
                        color: Colors.black38,
                        borderRadius: BorderRadius.circular(14)),
                    child:
                        Text(m, style: const TextStyle(color: Colors.white)),
                  ),
                ),
            ],
          ),
        ),
        SafeArea(
          child: Column(mainAxisSize: MainAxisSize.min, children: [
            SizedBox(
              height: 44,
              child: ListView(
                scrollDirection: Axis.horizontal,
                padding: const EdgeInsets.symmetric(horizontal: 8),
                children: [
                  for (var k = 0; k < fxs.length; k++)
                    Padding(
                      padding: const EdgeInsetsDirectional.only(end: 8),
                      child: ChoiceChip(
                        label: Text(fxs[k]),
                        selected: fx == k,
                        onSelected: (_) {
                          setState(() => fx = k);
                          say('المؤثر الصوتي: ${fxs[k]}');
                        },
                      ),
                    ),
                ],
              ),
            ),
            Padding(
              padding: const EdgeInsets.all(8),
              child: Row(children: [
                IconButton(
                  onPressed: () {
                    setState(() => mic = !mic);
                    say(mic
                        ? 'الميكروفون يعمل (عرض تجريبي)'
                        : 'تم كتم الميكروفون');
                  },
                  icon: Icon(mic ? Icons.mic : Icons.mic_off,
                      color: mic ? Colors.redAccent : Colors.white),
                ),
                IconButton(
                    onPressed: sendGift,
                    icon: const Text('🎁', style: TextStyle(fontSize: 26))),
                Expanded(
                  child: TextField(
                    controller: ctl,
                    style: const TextStyle(color: Colors.white),
                    decoration: InputDecoration(
                      hintText: 'اكتب تعليقاً…',
                      hintStyle: const TextStyle(color: Colors.white54),
                      filled: true,
                      fillColor: const Color(0xFF2A1450),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(99),
                          borderSide: BorderSide.none),
                    ),
                  ),
                ),
                IconButton(
                  onPressed: () {
                    if (ctl.text.trim().isNotEmpty) {
                      say('أنت: ${ctl.text.trim()}');
                      ctl.clear();
                    }
                  },
                  icon: const Icon(Icons.send, color: Colors.white),
                ),
              ]),
            ),
          ]),
        ),
      ]),
    );
  }
}
