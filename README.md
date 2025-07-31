import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

/// A reusable widget to display an SVG icon inside a styled card container.
///
/// Typically used for showing biller or brand logos.
/// Provides consistent padding, rounded corners, and error handling.
class BillerImage extends StatelessWidget {
  /// Path to the SVG asset to render.
  final String svgPath;

  /// Size of the card (width and height). Defaults to 60.
  final double size;

  const BillerImage({
    super.key,
    required this.svgPath,
    this.size = 60,
  });

  @override
  Widget build(BuildContext context) {
    return Container(
      width: size,
      height: size,
      padding: const EdgeInsets.all(10),
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(12),
        border: Border.all(
          color: Theme.of(context).primaryColor,
          width: 1,
        ),
      ),
      child: SvgPicture.asset(
        svgPath,
        fit: BoxFit.contain,
        placeholderBuilder: (_) =>
            const Icon(Icons.error_outline, color: Colors.red),
      ),
    );
  }
}