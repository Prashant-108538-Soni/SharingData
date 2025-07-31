import 'package:flutter/material.dart';

class ScrollableChipHeader extends StatefulWidget {
  final List<String> chipLabels;

  const ScrollableChipHeader({super.key, required this.chipLabels});

  @override
  State<ScrollableChipHeader> createState() => _ScrollableChipHeaderState();
}

class _ScrollableChipHeaderState extends State<ScrollableChipHeader> {
  final ScrollController _controller = ScrollController();
  bool _showLeft = false;
  bool _showRight = false;

  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addPostFrameCallback((_) => _checkScrollButtons());
    _controller.addListener(_checkScrollButtons);
  }

  void _checkScrollButtons() {
    setState(() {
      _showLeft = _controller.offset > 0;
      _showRight = _controller.offset < _controller.position.maxScrollExtent;
    });
  }

  void _scroll(double offset) {
    _controller.animateTo(
      _controller.offset + offset,
      duration: const Duration(milliseconds: 300),
      curve: Curves.easeInOut,
    );
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      height: 50,
      child: Stack(
        children: [
          Padding(
            padding: const EdgeInsets.symmetric(horizontal: 40),
            child: ListView.separated(
              controller: _controller,
              scrollDirection: Axis.horizontal,
              itemCount: widget.chipLabels.length,
              separatorBuilder: (_, __) => const SizedBox(width: 8),
              itemBuilder: (context, index) => Chip(
                label: Text(widget.chipLabels[index]),
                backgroundColor: Colors.grey[200],
                padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 8),
              ),
            ),
          ),
          if (_showLeft)
            Positioned(
              left: 0,
              top: 0,
              bottom: 0,
              child: Center(
                child: IconButton(
                  icon: const Icon(Icons.arrow_back_ios),
                  onPressed: () => _scroll(-100),
                ),
              ),
            ),
          if (_showRight)
            Positioned(
              right: 0,
              top: 0,
              bottom: 0,
              child: Center(
                child: IconButton(
                  icon: const Icon(Icons.arrow_forward_ios),
                  onPressed: () => _scroll(100),
                ),
              ),
            ),
        ],
      ),
    );
  }
}