import 'package:flutter/material.dart';
import 'package:flutter_svg/svg.dart';

/// A reusable widget that displays a status icon and accompanying text.
///
/// This widget is useful for showing status messages like "SmartPay Set"
/// with an svg icon (e.g., checkmark) and text aligned horizontally.
class Description extends StatelessWidget {

  /// Path to the SVG asset (e.g., "assets/icons/phone_bill.svg")
  final String svgPath;

  /// The text to be displayed next to the icon.
  final String text;

  /// Creates a [StatusIndicator] widget.
  ///
  /// [icon] and [text] are required.
  const Description({
    super.key,
    required this.svgPath,
    required this.text,
  });

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
          child: SizedBox(
            width: 10,
            height: 10,
            child: SvgPicture.asset(
              svgPath,
              // Add placeholderBuilder for error handling
              placeholderBuilder: (BuildContext context) =>
              const Icon(Icons.error_outline, color: Colors.red),
            ),
          ),
        ),
        const SizedBox(width: 8),

        // Text shown next to the icon
        Flexible(
          child: Text(
            text,
            style: const TextStyle(
              color: Colors.green,
              fontWeight: FontWeight.w600,
            ),
          ),
        ),
      ],
    );
  }
}
