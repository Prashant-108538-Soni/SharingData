import 'package:flutter/material.dart';

/// A reusable widget that displays a status icon and accompanying text.
/// 
/// This widget is useful for showing status messages like "SmartPay Set"
/// with an icon (e.g., checkmark) and text aligned horizontally.
class StatusIndicator extends StatelessWidget {
  /// The icon to be displayed on the left (e.g., a checkmark).
  final Icon icon;

  /// The text to be displayed next to the icon.
  final String text;

  /// Creates a [StatusIndicator] widget.
  ///
  /// [icon] and [text] are required.
  const StatusIndicator({
    Key? key,
    required this.icon,
    required this.text,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisSize: MainAxisSize.min,
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [
        // Icon shown inside a circle
        Container(
          decoration: BoxDecoration(
            shape: BoxShape.circle,
            border: Border.all(color: Colors.green, width: 2),
          ),
          padding: const EdgeInsets.all(4),
          child: icon,
        ),
        const SizedBox(width: 8),

        // Text shown next to the icon
        Text(
          text,
          style: const TextStyle(
            color: Colors.green,
            fontSize: 18,
            fontWeight: FontWeight.w600,
          ),
        ),
      ],
    );
  }
}