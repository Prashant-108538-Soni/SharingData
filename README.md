import 'package:flutter/material.dart';
import 'package:flutter_svg/svg.dart';

/// A compact widget that displays an icon alongside a status label.
///
/// Commonly used for showing small inline status indicators like
/// "SmartPay Set" or "AutoPay Enabled" with an SVG icon.
///
/// The icon is rendered inside a bordered circular container.
class Description extends StatelessWidget {
  /// Path to the SVG asset to be displayed.
  final String svgPath;

  /// Text displayed next to the icon.
  final String text;

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
        // Circular bordered icon
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
              placeholderBuilder: (_) =>
                  const Icon(Icons.error_outline, color: Colors.red),
            ),
          ),
        ),
        const SizedBox(width: 8),

        // Status text
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